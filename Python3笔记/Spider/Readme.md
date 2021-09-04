# 网络爬虫

> 网络爬虫，是一种按照一定的规则，自动地抓取万维网信息的程序或者脚本。——[百度百科](https://baike.baidu.com/item/%E7%BD%91%E7%BB%9C%E7%88%AC%E8%99%AB)

## 通用爬虫

> 通用网络爬虫又称全网爬虫（Scalable Web Crawler），爬行对象从一些种子 URL 扩充到整个 Web，主要为门户站点搜索引擎和大型 Web 服务提供商采集数据。——[百度百科](https://baike.baidu.com/item/%E7%BD%91%E7%BB%9C%E7%88%AC%E8%99%AB#3)

简单来说，通用爬虫就是实现网络搜索引擎的爬虫系统，如百度、必应、谷歌等等。

### 工作原理

尽可能将网络中的网页抓取到自己服务器形成备份，在对他们进行相应处理。

**搜索引擎获取新网站的方法**  

1. 提供提交新网站网址的网站收录网页（[百度链接提交](https://ziyuan.baidu.com/linksubmit/url)、[360提交](https://info.so.com/site_submit.html)）
2. 在其他网站里设置网站的外链。
3. 与DNS服务商合作

**搜索引擎规则**  

Robots协议：规定通用爬虫爬取网页权限  

[百度百科](https://baike.baidu.com/item/robots%E5%8D%8F%E8%AE%AE/2483797?fr=aladdin)

**缺点**  

1. 只能提供与文本相关的内容
2. 搜索结果不够个性化


## 聚焦爬虫

> 聚焦网络爬虫（Focused Crawler），是指选择性地爬行那些与预先定义好的主题相关页面的网络爬虫。 ——[百度百科](https://baike.baidu.com/item/%E7%BD%91%E7%BB%9C%E7%88%AC%E8%99%AB#3)


个人或小型公司写的爬虫。


