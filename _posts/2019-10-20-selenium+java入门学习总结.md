# 一、selenium简介
- Selenium是一个用于Web应用程序测试的工具。Selenium测试直接运行在浏览器中，就像真正的用户在操作一样。支持的浏览器包括IE（7, 8, 9, 10, 11），Mozilla Firefox，Safari，Google Chrome，Opera等。这个工具的主要功能包括：测试与浏览器的兼容性——测试你的应用程序看是否能够很好得工作在不同浏览器和操作系统之上。测试系统功能——创建回归测试检验软件功能和用户需求。支持自动录制动作和自动生成 .Net、Java、Perl、python等不同语言的测试脚本。

# 二、selenium简单使用
## 1.新建maven项目
- 依赖
`<dependency>
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
</dependency>
`
## 2.下载驱动
- Selenium需要驱动程序才能与所选浏览器交互.驱动程序下载地址:
- Chrome:	https://sites.google.com/a/chromium.org/chromedriver/downloads
- Edge:	https://developer.microsoft.com/en-us/microsoft-edge/tools/webdriver/
- Firefox:	https://github.com/mozilla/geckodriver/releases
- Safari:	https://webkit.org/blog/6900/webdriver-support-in-safari-10/
- 注：不同版本的浏览器对应不同版本的驱动，一定要保证浏览器和驱动版本对应。
      下载好的驱动需要加入环境变量中。

## 3.编写自动化脚本
- 编写简单的打开百度搜索selenium的自动化脚本
  `    @Test
    public void testSelenium() throws InterruptedException {
        //打开浏览器
        WebDriver webDriver = new ChromeDriver();
        //最大化窗口
        webDriver.manage().window().maximize();
        //导航百度
        webDriver.get("https://www.baidu.com");
        //隐式等待5秒
        webDriver.manage().timeouts().implicitlyWait(5, TimeUnit.SECONDS);
        //输入selenium
        webDriver.findElement(By.id("kw")).sendKeys("selenium");
        //点击百度一下
        webDriver.findElement(By.cssSelector(".quickdelete-wrap")).click();
        //强制等待5秒
        Thread.sleep(5000);
        //退出
        webDriver.quit();
    }
  `
## 4.定位元素
- 定位元素的方法如下：
- `find_element_by_id` 通过id定位
- `find_element_by_name` 通过name定位
- `find_element_by_xpath`  通过xpath定位
- `find_element_by_link_text` 通过链接文本定位
- `find_element_by_partial_link_text`  
- `find_element_by_tag_name`  通过标签定位
- `find_element_by_class_name`  通过class定位
- `find_element_by_css_selector`  通过css定位

## 5.等待方式
- Selenium Webdriver提供两种类型的等待-隐式和显式。
- 显示等待:客户端轮询查找，每找一次元素，等待一个间隔再次查找，知道条件匹配，一次性的。
`WebDriverWait(driver, 10).until(
                  EC.presence_of_element_located((By.ID,location))
              )`
- 隐式等待：服务端会帮你轮询查找，全局性的
 `driver.implicitly_wait(10)`
- 极端情况下也可以使用强制等待方式
`time.sleep（）`
- 例：

## 6.心得
- 到这里selenium已经入门啦，想要高效率、准确性地跑测试用例进行web自动化测试就需要对方法、用例进行封装改造，采用PO模式来进行框架的封装。
- selenium
- PO原则
    The public methods represent the services that the page offers
    Try not to expose the internals of the page
    Generally don't make assertions
    Methods return other PageObjects
    Need not represent an entire page
    Different results for the same action are modelled as different methods
- 参考文档
 https://selenium-python.readthedocs.io
