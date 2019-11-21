# 一、selenium简介
- Selenium是一个用于Web应用程序测试的工具。Selenium测试直接运行在浏览器中，就像真正的用户在操作一样。支持的浏览器包括IE（7, 8, 9, 10, 11），Mozilla Firefox，Safari，Google Chrome，Opera等。这个工具的主要功能包括：测试与浏览器的兼容性——测试你的应用程序看是否能够很好得工作在不同浏览器和操作系统之上。测试系统功能——创建回归测试检验软件功能和用户需求。支持自动录制动作和自动生成 .Net、Java、Perl、python等不同语言的测试脚本。

# 二、selenium简单使用
## 1.新建maven项目
- 加入依赖
```<dependency>
      <groupId>org.seleniumhq.selenium</groupId>
      <artifactId>selenium-api</artifactId>
      <version>3.141.59</version>
      <scope>test</scope>
 </dependency>
 <dependency>
      <groupId>org.seleniumhq.selenium</groupId>
      <artifactId>selenium-chrome-driver</artifactId>
      <version>3.141.59</version>
      <scope>test</scope>
  </dependency>```
  
## 2.下载驱动
- Selenium需要驱动程序才能与所选浏览器交互.驱动程序下载地址:
- Chrome:	[Chromedriver下载地址](https://sites.google.com/a/chromium.org/chromedriver/downloads)
- Edge:	[webdriver下载地址](https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/)
- Firefox:	[geckodriver下载地址](https://github.com/mozilla/geckodriver/releases)
- Safari:	[下载地址](https://webkit.org/blog/6900/webdriver-support-in-safari-10/)
- 注：不同版本的浏览器对应不同版本的驱动，一定要保证浏览器和驱动版本对应。
      下载好的驱动需要加入环境变量中。
      部分浏览器驱动地址需要科学上网

## 3.编写自动化脚本
- 编写简单的打开百度搜索selenium的自动化脚本
-  #打开浏览器
-  `WebDriver webDriver = new ChromeDriver();`
-  #窗口最大化
-  `webDriver.manage().window().maximize();`
-  #打开百度
-  `webDriver.get("https://www.baidu.com");`
-  #隐式等待5秒
-  `webDriver.manage().timeouts().implicitlyWait(5, TimeUnit.SECONDS);`
-  #输入框输入selenium
-  `webDriver.findElement(By.id("kw")).sendKeys("selenium");`
-  #点击百度一下
-  `webDriver.findElement(By.cssSelector(".s_btn")).click();`
-  #刷新网页
-  `webDriver.navigate().refresh();`
-  #等待5秒
-  `Thread.sleep(5000);`
-  #退出
-  `webDriver.quit();`

## 4.定位元素
- 8种定位元素的方法：
- `findElement(By.id())` 通过id定位
- `findElement(By.name())` 通过name定位
- `findElement(By.xpath())`  通过xpath定位
- `findElement(By.linkText())` 通过链接文本定位
- `findElement(By.partialLinkText())`  
- `findElement(By.tagName())`  通过标签定位
- `findElement(By.className())`  通过class定位
- `findElement(By.cssSelector())`  通过css定位，web自动化用css一般都能解决

## 5.常用API
- `maximize()` 设置浏览器最大化
- `setSize()` 设置浏览器宽高
- `clear()` 清除文本
- `sendKeys(*value)` 模拟按键输入
- `click()` 单击元素
- `getSize()` 返回元素的尺寸
- `getText()` 获取元素的文本
- `getAttribute(name)` 获得属性值
- `new Actions().contextClick()` 右击
- `new Actions().clickAndHold()` 鼠标点击并控制
- `new Actions().doubleClick()` 双击
- `new Actions().dragAndDrop()` 拖动
- `new Actions().release()` 释放鼠标
- `getTitle()` 用于获得当前页面的title。
- `getCurrentUrl()` 用户获得当前页面的URL。
- `getText()` 获取页面文本信息。
- `switchTo().frame()` 多表单切换
- `switchTo().window()` 多窗口切换
- `new Select(el).selectByValue()` 选择框
- `getCookies()` 获得所有 cookie 信息
- `executeScript()` 执行JavaScript代码。
