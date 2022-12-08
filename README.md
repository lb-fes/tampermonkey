# 官方网站

https://www.tampermonkey.net/index.php?ext=dhdg#google_vignette

# 官方帮助文档

https://www.tampermonkey.net/documentation.php

TamperMonkey 可使用的 API 和 GreaseMonkey 的区别

## @name

脚本名字（支持中文）

```javascript
// @name 脚本名
// @name:zh-CN 本地化？
```

## @namespace

脚本的命名空间

脚本地址

## @version

脚本版本。这用于更新检查，以防脚本不是从 userscript.org 安装的，或者 TM 在检索脚本元数据时遇到问题。

## @description

简单明了的描述脚本功能

## @author

作者名字或网址

## @match

作用的网址

## @grant

@grant 用于将 GM_* 函数、unsafeWindow 对象和一些有用的窗口函数列入白名单。如果没有写@grant 标签，TM 会猜测脚本需要的 @grant。

```javascript
// @grant GM_setValue
// @grant GM_getValue
// @grant GM_setClipboard
// @grant unsafeWindow
// @grant window.close
// @grant window.focus
// @grant window.onurlchange
```

由于关闭和聚焦选项卡是一项强大的功能，因此也需要将其添加到 @grant 语句中。

如果脚本在单页应用程序上运行，那么它可以使用 window.onurlchange 来监听 URL 变化：

```javascript
// ==UserScript==
...
// @grant window.onurlchange
// ==/UserScript==

if (window.onurlchange === null) {
    // feature is supported
    window.addEventListener('urlchange', (info) => ...);
}
```

如果@grant 后跟 'none'，则 `sandbox` 被禁用并且脚本将直接在页面上下文中运行。在这种模式下，没有 GM_* 功能，但 GM_info 属性可用。

```javascript
// @grant none
```

### GM_xmlhttpRequest(details)

Make an xmlHttpRequest.

详细属性:

- **method** one of GET, HEAD, POST

- **url** 目的地 URL

- **headers** ie. user-agent, referer, ... (Safari and Android 浏览器 不支持一些特殊的 headers )

- **data** 通过 POST 请求发送的一些字符串

- **cookie** 要修补到已发送的 cookie 集中的 cookie

- **binary** 以二进制方式发送数据字符串

- **nocache** 不要缓存资源

- **revalidate** 重新验证可能缓存的内容

- **timeout** 以 `ms` 为单位的超时

- **context** 会被添加到 response object 的属性

- **responseType** arraybuffer, blob, json or stream 中的一个

- **overrideMimeType** a MIME type for the request

- **anonymous** 不要随请求发送 cookie (请看 the fetch notes)

- **fetch** (beta) use a fetch instead of a xhr request
  (在谷歌浏览器中这可能导致 details.timeout and xhr.onprogress 无法工作 and makes xhr.onreadystatechange receive only readyState 4 events)

- **user** 用于身份验证的用户名

- **password** 密码

- **onabort** callback to be executed if the request was aborted

- **onerror** callback to be executed if the request ended up with an error

- **onloadstart** callback to be executed on load start, provides access to the stream object if responseType is set to "stream"

- **onprogress** callback to be executed if the request made some progress

- **onreadystatechange** callback to be executed if the request's ready state changed

- **ontimeout** callback to be executed if the request failed due to a timeout

- onload

   

  callback to be executed if the request was loaded.

  It gets one argument with the following attributes:

  - **finalUrl** - the final URL after all redirects from where the data was loaded
  - **readyState** - the ready state
  - **status** - the request status
  - **statusText** - the request status text
  - **responseHeaders** - the request response headers
  - **response** - the response data as object if *details.responseType* was set
  - **responseXML** - the response data as XML document
  - **responseText** - the response data as plain string

Returns an object with the following property:

- **abort** - function to be called to cancel this request


**Note:** the **synchronous** flag at *details* is not supported

**Important:** if you want to use this method then please also check the documentation about [@connect](https://www.tampermonkey.net/documentation.php#_connect).

国际化翻译：https://github.com/Tampermonkey/tampermonkey-i18n