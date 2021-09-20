<h1 align="center">Fofa_Viewer 🔗 </h1>
<p align="center"> 
<img src="https://img.shields.io/badge/JDK-1.8-green">
<img src="https://img.shields.io/badge/version-1.0.8-brightgreen">
<img src="https://img.shields.io/badge/author-f1ashine-orange">
<img src="https://img.shields.io/badge/WgpSec-%E7%8B%BC%E7%BB%84%E5%AE%89%E5%85%A8%E5%9B%A2%E9%98%9F-blue">
</p>


中文 | [EN](README.en.md)

##  简介

Fofa_Viewer 一个简单易用的fofa客户端由WgpSec狼组安全团队 [**f1ashine**](https://github.com/f1ashine) 师傅主要编写 ，程序使用使用javafx编写，便于跨平台使用

##  使用

下载最新版本包，修改`config.properties` 即可开始使用

Mac 用户可通过 [自动化操作创建应用程序](docs/mac.md) 进行快速启动 Fofa_Viewer


**若下载速度太慢可以使用**

https://hub.fastgit.org/wgpsec/fofa_viewer (推荐)

https://gitee.com/wgpsec/fofa_viewer （镜像）

## :sparkles: 功能
1. 多标签式查询结果展示
2. 丰富的右键菜单
3. 支持查询结果导出为excel文件
4. 支持手动修改查询最大条数，方便非高级会员使用(修改`config.properties`中的`maxSize`即可)
5. 支持证书转换 将证书序列填写入启动页框内可转换，再使用 `cert="计算出来的值"` 语法进行查询 [具体例子](https://mp.weixin.qq.com/s/jBf9h6IQVja6WwFcSYEvKg)
6. 支持输入智能提示
7. 支持fofa的一键排除干扰（蜜罐）功能。（注：需要高级会员才能使用，使用时会在tab页标记`(*)`）
8. 显示fofa官网的查询语法

![](docs/ui.png)
![](docs/search.jpg)

## Q&A
1. 为什么查询显示结果超过了10000条，但是导出的数据不到10000条？  
  由于fofa api的限制，每个查询条件最多获取10000条数据，所以超过10000条以后的数据将无法导出，可尝试通过关键字`after`和`before`限制查询时间来获取数据。

2. 为什么界面显示和excel导出的数据比查询到的数据要少？  
  由于fofa查询到的http数据中有部分数据重复，为了二次扫描和查看方便，工具做了去重处理，具体分为以下四种情况:
  - 端口为80：去掉协议头显示为http的数据
    ![](docs/80http.png)
  - 端口为443：
    ![](docs/443https.png)
  - 非80端口的http
    ![](docs/非80http.png)
  - 非443端口的https
    ![](docs/非443https.png)
    
3. 为什么有的网站明明有favicon但是请求不到？  
  说一下浏览器获取favicon的流程：  
   ① 先去html的header标签中提取`<link rel=icon href=xx>`，然后加载href中的链接  
   ② 如果没有link标签，浏览器会加载根目录的`favicon.ico`，如果响应404就代表网站未提供favicon  
  本工具使用的是`jsoup`对网页进行解析，对于使用Vue一类构建的网站只能通过chrome进行js解析后获取link标签然后获取favicon地址，对于这种情况目前只能将favicon的链接粘贴到首页进行查询。
   
4. IP和端口两个一起排序？  
  先点击IP或者端口这一列的header进行排序，然后按住shift点击另一列就可以一起排序了

## :rocket: 二次开发
```
git clone https://github.com/wgpsec/fofa_viewer.git
```

本项目使用 `maven-assembly-plugin`打包编译，可按照下图进行配置

![](docs/compile_detail.png)

idea打开项目，等待依赖包下载完毕后直接双击Plugins-assembly-assembly:assembly，然后将target文件夹中带有"with-dependencies"的jar包拷贝到带有config.properties的文件夹再运行即可。

![](docs/maven_detail.png)



## ⚠️ 说明
- 使用前需要在`config.properties`中配置`email`和`key`才能正常使用
- 项目中配置了error.log，如果有需要提bug，希望能带上这个截图，另外也欢迎提issue帮助改进。
- 如果出现了bug，不知道哪出错了，也可以在终端使用`java -jar fofaviewer.jar`启动，出错后终端会显示具体的错误详情，提交issue的时候请带上截图。
- 关注公众号回复 “加群” 即可加入官方交流群

![](https://assets.wgpsec.org/www/images/wechat.png)

[![Stargazers over time](https://starchart.cc/wgpsec/fofa_viewer.svg)](https://starchart.cc/wgpsec/fofa_viewer)


