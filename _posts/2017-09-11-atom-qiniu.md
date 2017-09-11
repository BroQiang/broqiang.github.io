---
layout: post
title: 'Atom 配置七牛云图床'
date: '2017-09-11'
header-img: "img/post-bg-unix.jpg"
author: 'Bro Qiang'
---

# Atom 配置七牛云图床

## 安装 插件

一直纠结 markdown 写文档没有好的解决图片的办法，偶然间发现了一个 图床，试用了下非常好用，不过只找到了 `atom` 的插件，所以以后就用它来写 `markdown` 文档了。

要想使用 七牛云的图床需要安装两个插件，`markdown-assistant` 和 `qiniu-uploader`，有两种方式安装：

#### 方法1： 终端中使用命令安装

打开终端，输入下面命令：

```shell
apm install markdown-assistant
apm install qiniu-uploader
```

#### 方法2： 直接在 `Atom` 中安装

`Ctrl+Shift+P` ，输入 `install Packages And Themes` ，如图：

![打开设置](http://image.broqiang.com/2b0696ee14aa2f8a2f19bb1be2ddacbb.png)

然后分别输入 `markdown-assistant` 和 `qiniu-uploaderqiniu-uploader`，搜索插件安装，如图
然后分别输入 `markdown-assistant` 和 `qiniu-uploaderqiniu-uploader`，搜索插件安装，如图

![安装插件](http://image.broqiang.com/9ed3c936d9e5edf8afb23a57796690e9.png)


## 配置 qiniu-uploader

#### 七牛云配置

- 到 [七牛云官方](http://qiniu.com) 注册账号，并创建一个对象存储的，其中的新建存储空间的名字就是后面配置文件中的 `qiniuBucket`，右侧的域名就是配置文件中的 `qiniuDomain`，如图：

    ![配置](http://image.broqiang.com/e65633a74d1f689a924b075bca8c6354.png)

- 获取 `AK` 和 `SK`

    点击右上角的 `个人面板` 下的 `密钥管理`，在新的页面中点击 `创建密钥`，就会生成 `AK` 和 `SK` ，如图：

![获取key](http://image.broqiang.com/2474b9bfca7458b38704dc8ab7531b3f.png)

#### 配置 qiniu-uploader setting

在 Settings 中找到 qiniu-uploader ，然后点击 Settings，如图：

![settings](http://image.broqiang.com/7b4e24c58febac6510172037ea4fd3e1.png)

然后写入七牛云的配置文件，配置文件中的内容就是上面介绍的内容中找到的，如图：

![configFile](http://image.broqiang.com/6cbb4a030317360dca6b47d4d0bb7e32.png)

## 解决 bug

插件安装完成之后有可能会没有 Settings 按钮，并会在启动的时候报错：

![error](http://image.broqiang.com/da79c8140fd97dc4248e3d616d06b3a9.png)

原本的 插件有bug，个人猜测是七牛的 sdk 更新了，插件没有更新，需要手动替换三个文件，这个三个文件在 `~/.atom/packages/qiniu-uploader/node_modules/qiniu/qiniu` 目录中，这三个文件分别是 ：

> 为了方便，直接贴的代码

- os.js

```js
var conf = require('./conf');
var util = require('./util');
var rpc = require('./rpc');
var fs = require('fs');
var getCrc32 = require('crc32');
var url = require('url');
var mime = require('mime');
var Readable = require('stream').Readable;
var formstream = require('formstream');
var urllib = require('urllib');
var zone = require('./zone');
exports.UNDEFINED_KEY = '?'
exports.PutExtra = PutExtra;
exports.PutRet = PutRet;
exports.put = put;
exports.putWithoutKey = putWithoutKey;
exports.putFile = putFile;
exports.putReadable = putReadable;
exports.putFileWithoutKey = putFileWithoutKey;
// @gist PutExtra
function PutExtra(params, mimeType, crc32, checkCrc) {
    this.params = params || {};
    this.mimeType = mimeType || null;
    this.crc32 = crc32 || null;
    this.checkCrc = checkCrc || 0;
}
// @endgist
function PutRet(hash, key) {
    this.hash = hash || null;
    this.key = key || null;
}
// onret: callback function instead of ret
function putReadable(uptoken, key, rs, extra, onret) {
    if (!extra) {
        extra = new PutExtra();
    }
    if (!extra.mimeType) {
        extra.mimeType = 'application/octet-stream';
    }
    if (!key) {
        key = exports.UNDEFINED_KEY;
    }
    rs.on("error", function(err) {
        onret({ code: -1, error: err.toString() }, {});
    });
    // 设置上传域名
    // zone.up_host(uptoken, conf);
    zone.up_host_async(uptoken, conf, function() {
        var form = getMultipart(uptoken, key, rs, extra);
        return rpc.postMultipart(conf.UP_HOST, form, onret);
    });
}

function put(uptoken, key, body, extra, onret) {
    var rs = new Readable();
    rs.push(body);
    rs.push(null);
    if (!extra) {
        extra = new PutExtra();
    }
    if (extra.checkCrc == 1) {
        var bodyCrc32 = getCrc32(body);
        extra.crc32 = '' + parseInt(bodyCrc32, 16);
    } else if (extra.checkCrc == 2 && extra.crc32) {
        extra.crc32 = '' + extra.crc32
    }
    return putReadable(uptoken, key, rs, extra, onret)
}

function putWithoutKey(uptoken, body, extra, onret) {
    return put(uptoken, null, body, extra, onret);
}

function getMultipart(uptoken, key, rs, extra) {
    var form = formstream();
    form.field('token', uptoken);
    if (key != exports.UNDEFINED_KEY) {
        form.field('key', key);
    }
    form.stream('file', rs, key, extra.mimeType);
    if (extra.crc32) {
        form.field('crc32', extra.crc32);
    }
    for (var k in extra.params) {
        form.field(k, extra.params[k]);
    }
    return form;
}

function putFile(uptoken, key, loadFile, extra, onret) {
    var rs = fs.createReadStream(loadFile);
    if (!extra) {
        extra = new PutExtra();
    }
    if (extra.checkCrc == 1) {
        var fileCrc32 = getCrc32(fs.readFileSync(loadFile));
        extra.crc32 = '' + parseInt(fileCrc32, 16);
    } else if (extra.checkCrc == 2 && extra.crc32) {
        extra.crc32 = '' + extra.crc32
    }
    if (!extra.mimeType) {
        extra.mimeType = mime.lookup(loadFile);
    }
    return putReadable(uptoken, key, rs, extra, onret);
}

function putFileWithoutKey(uptoken, loadFile, extra, onret) {
    return putFile(uptoken, null, loadFile, extra, onret);
}
```

- rpc.js

```JavaScript
var urllib = require('urllib');
var util = require('./util');
var conf = require('./conf');
exports.postMultipart = postMultipart;
exports.postWithForm = postWithForm;
exports.postWithoutForm = postWithoutForm;

function postMultipart(uri, form, onret) {
    return post(uri, form, form.headers(), onret);
}

function postWithForm(uri, form, token, onret) {
    var headers = {
        'Content-Type': 'application/x-www-form-urlencoded'
    };
    if (token) {
        headers['Authorization'] = token;
    }
    return post(uri, form, headers, onret);
}

function postWithoutForm(uri, token, onret) {
    var headers = {
        'Content-Type': 'application/x-www-form-urlencoded',
    };
    if (token) {
        headers['Authorization'] = token;
    }
    return post(uri, null, headers, onret);
}

function post(uri, form, headers, onresp) {
    headers = headers || {};
    headers['User-Agent'] = headers['User-Agent'] || conf.USER_AGENT;
    var data = {
        headers: headers,
        method: 'POST',
        dataType: 'json',
        timeout: conf.RPC_TIMEOUT,
    };
    if (Buffer.isBuffer(form) || typeof form === 'string') {
        data.content = form;
    } else if (form) {
        data.stream = form;
    } else {
        data.headers['Content-Length'] = 0;
    };
    var req = urllib.request(uri, data, function(err, result, res) {
        var rerr = null;
        if (err || Math.floor(res.statusCode / 100) !== 2) {
            rerr = { code: res && res.statusCode || -1, error: err || result && result.error || '' };
        }
        onresp(rerr, result, res);
    });
    return req;
}
```

- zone.js

```js
// var request = require('urllib-sync').request;
var urllib = require('urllib');
var util = require('./util');
//conf 为全局变量
exports.up_host = function(uptoken, conf) {
    var version = process.versions;
    var num = version.node.split(".")[0];
    // node 版本号低于 1.0.0, 使用默认域名上传，可以在conf中指定上传域名
    if (num < 1) {
        conf.AUTOZONE = false;
    }
    if (!conf.AUTOZONE) {
        return;
    }
    var ak = uptoken.toString().split(":")[0];
    var tokenPolicy = uptoken.toString().split(":")[2];
    var tokenPolicyStr = new Buffer(tokenPolicy, 'base64').toString();
    var json_tokenPolicyStr = JSON.parse(tokenPolicyStr);
    var scope = json_tokenPolicyStr.scope;
    var bucket = scope.toString().split(":")[0];
    // bucket 相同，上传域名仍在过期时间内
    if ((new Date().getTime() < conf.EXPIRE) && bucket == conf.BUCKET) {
        return;
    }
    //记录bucket名
    conf.BUCKET = bucket;
    var request_url = 'http://uc.qbox.me/v1/query?ak=' + ak + '&bucket=' + bucket;
    var res = request('http://uc.qbox.me/v1/query?ak=' + ak + '&bucket=' + bucket, {
        'headers': {
            'Content-Type': 'application/json'
        }
    });
    if (res.statusCode == 200) {
        var json_str = JSON.parse(res.body.toString());
        //判断设置使用的协议, 默认使用http
        if (conf.SCHEME == 'http') {
            conf.UP_HOST = json_str.http.up[1];
        } else {
            conf.UP_HOST = json_str.https.up[0];
        }
        conf.EXPIRE = 86400 + new Date().getTime();
    } else {
        var err = new Error('Server responded with status code ' + res.statusCode + ':\n' + res.body.toString());
        err.statusCode = res.statusCode;
        err.headers = res.headers;
        err.body = res.body;
        throw err;
    }
}
exports.up_host_async = function(uptoken, conf, callback) {
    var version = process.versions;
    var num = version.node.split(".")[0];
    // node 版本号低于 1.0.0, 使用默认域名上传，可以在conf中指定上传域名
    if (num < 1) {
        conf.AUTOZONE = false;
    }
    if (!conf.AUTOZONE) {
        callback();
        return;
    }
    var ak = uptoken.toString().split(":")[0];
    var tokenPolicy = uptoken.toString().split(":")[2];
    var tokenPolicyStr = new Buffer(tokenPolicy, 'base64').toString();
    var json_tokenPolicyStr = JSON.parse(tokenPolicyStr);
    var scope = json_tokenPolicyStr.scope;
    var bucket = scope.toString().split(":")[0];
    // bucket 相同，上传域名仍在过期时间内
    if ((new Date().getTime() < conf.EXPIRE) && bucket == conf.BUCKET) {
        callback();
        return;
    }
    //记录bucket名
    conf.BUCKET = bucket;
    var request_url = 'http://uc.qbox.me/v1/query?ak=' + ak + '&bucket=' + bucket;
    var data = {
        contentType: 'application/json',
        method: 'GET',
    };
    var req = urllib.request(request_url, data, function(err, result, res) {
        // console.log(result);
        if (res.statusCode == 200) {
            // console.log(result);
            var json_str = JSON.parse(result.toString());
            // console.log(json_str);
            //判断设置使用的协议, 默认使用http
            if (conf.SCHEME == 'http') {
                conf.UP_HOST = json_str.http.up[1];
            } else {
                conf.UP_HOST = json_str.https.up[0];
            }
            conf.EXPIRE = 86400 + new Date().getTime();
            callback();
            return;
        } else {
            var err = new Error('Server responded with status code ' + res.statusCode + ':\n' + res.body.toString());
            err.statusCode = res.statusCode;
            err.headers = res.headers;
            err.body = res.body;
            throw err;
            callback();
        }
    });
    return;
}
```









