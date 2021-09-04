# urllib

urllib 是一个收集了多个涉及 URL 的模块的包：

* [urllib.request](#request) 打开和读取 URL

* [urllib.error](#error) 包含 urllib.request 抛出的异常

* [urllib.parse](#parse) 用于解析 URL

* [urllib.robotparser](#robotparser) 用于解析 robots.txt 文件


## request

> An extensible library for opening URLs using a variety of protocols
> 
> The simplest way to use this module is to call the urlopen function, which accepts a string containing a URL or a Request object (described
below).  It opens the URL and returns the results as file-like object; the returned object has some extra methods described below.
> 
> The OpenerDirector manages a collection of Handler objects that do all the actual work.  Each Handler implements a particular protocol or
option.  The OpenerDirector is a composite object that invokes the Handlers needed to open the requested URL.  For example, the HTTPHandler performs HTTP GET and POST requests and deals with
non-error returns.  The HTTPRedirectHandler automatically deals with HTTP 301, 302, 303 and 307 redirect errors, and the HTTPDigestAuthHandler
deals with digest authentication.
> 
> urlopen(url, data=None) -- Basic usage is the same as original urllib.  pass the url and optionally data to post to an HTTP URL, and
get a file-like object back.  One difference is that you can also pass a Request instance instead of URL.  Raises a URLError (subclass of
OSError); for HTTP errors, raises an HTTPError, which can also be treated as a valid response.
> 
> build_opener -- Function that creates a new OpenerDirector instance.
> Will install the default handlers.  Accepts one or more Handlers as arguments, either instances or Handler classes that it will instantiate.  If one of the argument is a subclass of the default
handler, the argument will be installed instead of the default.
> 
> install_opener -- Installs a new opener as the default opener.
> 
> objects of interest:
> 
> OpenerDirector -- Sets up the User Agent as the Python-urllib client and manages the Handler classes, while dealing with requests and responses.
> 
> Request -- An object that encapsulates the state of a request.  The state can be as simple as the URL.  It can also include extra HTTP
headers, e.g. a User-Agent.
> 
> BaseHandler --
> 
>internals:  
> BaseHandler and parent  
> _call_chain conventions

Example usage:
```py
import urllib.request

# set up authentication info
authinfo = urllib.request.HTTPBasicAuthHandler()
authinfo.add_password(realm='PDQ Application',
                      uri='https://mahler:8092/site-updates.py',
                      user='klem',
                      passwd='geheim$parole')

proxy_support = urllib.request.ProxyHandler({"http" : "http://ahad-haam:3128"})

# build a new opener that adds authentication and caching FTP handlers
opener = urllib.request.build_opener(proxy_support, authinfo,
                                     urllib.request.CacheFTPHandler)

# install it
urllib.request.install_opener(opener)

f = urllib.request.urlopen('http://www.python.org/')
```
*注：以上引用源码注释*

### urlopen

`
urlopen(url, data=None, timeout=socket._GLOBAL_DEFAULT_TIMEOUT, *, cafile=None, capath=None, cadefault=False, context=None)
`  
url：要爬取的网址，要包含http(s)  
data：发送请求时携带的数据，对象类型，为None时为get请求，否则为post请求  
timeout：请求超时时间，单位秒  
cafile：证书相关  
capath：证书相关  
cadefault：The *cadefault* parameter is ignored.  
context：If *context* is specified, it must be a ssl.SSLContext instance describing the various SSL options. See HTTPSConnection for more details.  

    This function always returns an object which can work as a context manager and has methods such as

    * geturl() - return the URL of the resource retrieved, commonly used to determine if a redirect was followed

    * info() - return the meta-information of the page, such as headers, in the form of an email.message_from_string() instance (see Quick Reference to HTTP Headers)

    * getcode() - return the HTTP status code of the response.  Raises URLError on errors.

```py
from urllib import request

# 类似文件对象
response = request.urlopen('http://www.baidu.com/')

print(response.info())
print(response.read())
```

## error



## parse


### urlencode

> 将字典或两个元素元组序列编码为URL查询字符串。


`urlencode(query, doseq=False, safe='', encoding=None, errors=None, quote_via=quote_plus)`

**query**：包含请求参数的字典或元素为包含两个元素的元组的序列（sequence of two-element tuples）  
**deseq**：If the query arg is a sequence of two-element tuples, the order of the parameters in the output will match the order of parameters in the input. 还是看例子吧（[解码网址](http://tool.chinaz.com/tools/urlencode.aspx)）  

    In [11]: a = (1, '威威')

    In [13]: b = (2, '第三方')

    In [14]: parse.urlencode([a, b], doseq=True)
    Out[14]: '1=%E5%A8%81%E5%A8%81&2=%E7%AC%AC%E4%B8%89%E6%96%B9'

    In [15]: parse.urlencode([a], doseq=True)
    Out[15]: '1=%E5%A8%81%E5%A8%81'

    In [16]: parse.urlencode({1: ['无', '浏览'], 2: [32]}, doseq=True)
    Out[16]: '1=%E6%97%A0&1=%E6%B5%8F%E8%A7%88&2=32'

    In [17]: parse.urlencode({1: ['无', '浏览'], 2: [32, 4]}, doseq=True)
    Out[17]: '1=%E6%97%A0&1=%E6%B5%8F%E8%A7%88&2=32&2=4'

    In [18]: parse.urlencode({1: ['无', '浏览'], 2: [32, 4]})
    Out[18]: '1=%5B%27%E6%97%A0%27%2C+%27%E6%B5%8F%E8%A7%88%27%5D&2=%5B32%2C+4%5D'

    In [19]: parse.urlencode({1: ['无', '浏览'], 2: (1, 4)}, doseq=True)
    Out[19]: '1=%E6%97%A0&1=%E6%B5%8F%E8%A7%88&2=1&2=4'

    In [20]: parse.urlencode((a, b), doseq=True)
    Out[20]: '1=%E5%A8%81%E5%A8%81&2=%E7%AC%AC%E4%B8%89%E6%96%B9'

  
quote_via：应该是设置具体的转码函数，safe、encoding、errors都是被指定函数的参数  

*浏览器向服务器发送的url中只能包含单字节字符，所以要将多字节字符转码。*





## robotparser
