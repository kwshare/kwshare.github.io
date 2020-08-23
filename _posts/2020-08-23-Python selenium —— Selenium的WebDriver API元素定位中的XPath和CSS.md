---
layout: post
title:  "Selenium的WebDriver API元素定位中的XPath和CSS"
date:   2020-08-23 20:55:10
categories: Python selenium
permalink: /archivers/how-ti-use-Selenium-for-XPath-and-CSS
---

元素的定位和操作是自动化测试的核心部分，其中操作又是建立在定位的基础上的。

本文百度页面为例子，带入深入了解XPath和CSS定位的所有方法，代码较多，文字只提示重点关注的地方！！！

# 浏览器的常规操作
```python
import time
from selenium import webdriver

# 打开浏览器
driver = webdriver.Chrome()

# 加载网页
driver.get("https://www.baidu.com")
# 休息3秒
time.sleep(3)

# 设置浏览器最大化
driver.maximize_window()
time.sleep(2)

# 设置浏览器最小化
driver.minimize_window()
time.sleep(2)

# 设置浏览器窗口大小
driver.set_window_size(1200, 700)
time.sleep(2)

# 刷新
driver.refresh()
time.sleep(2)

# 返回
driver.back()
time.sleep(2)

# 前进
driver.forward()
time.sleep(2)

# 截图
driver.save_screenshot('baidu.png')
driver.get_screenshot_as_file('baidu2.png')

# 获取浏览器当前url
# print(driver.current_url)
print(f'浏览器当前URL:{driver.current_url}')  # https://www.baidu.com/

# 获取浏览器的标题title
# print(driver.title)
print(f'浏览器的标题:{driver.title}')  # 百度一下，你就知道

# 获取页面源码
print(driver.page_source)

# 关闭当前窗口
driver.close()

# 退出driver,关闭所有窗口
driver.quit()
```

# 八大元素定位方法
1、id定位

2、name定位

3、class_name定位

4、link_text定位(针对a标签)

5、partial_link_text定位(针对a标签)

6、tag_name标签名定位

7、xpath定位

（1）绝对路径（绝对路径使用"/"）

（2）相对路径（相对路径使用"//"）

（3）索引定位

> 1）具体格式：//标签名[@属性="属性值"]
> 2）支持使用and和or关键字，多个属性一起定位元素。

（4）属性定位

（5）部分的属性值

（6）通过文本定位

（7）各种xpath组合

（8）通配符*

8、css选择器定位

（1）绝对路径

（2）相对路径

（3）通过属性定位

（4）通过部分属性值（也称为模糊方法定位）

（5）通过查询子元素

（6）查找兄弟元素

## id定位
```python
# driver.find_element_by_id("kw").send_keys("测试玉米君")
# 输出获取到的元素的id属性内容
# print(driver.find_element_by_id("kw").get_attribute("id"))
print(f'1、id定位 获取到的元素的id属性内容:{driver.find_element_by_id("kw").get_attribute("id")}')  # kw
```


## name定位
```python
# driver.find_element_by_name('wd').send_keys("测试玉米君")
# 输出获取到的元素的name属性内容
# print(driver.find_element_by_name("wd").get_attribute("name"))
print(f'2、name定位 获取到的元素的name属性内容:{driver.find_element_by_name("wd").get_attribute("name")}')  # wd
```


## class_name定位
```python
# driver.find_element_by_class_name("s_ipt").send_keys("测试玉米君")
# 输出获取到的元素的class属性内容
# print(driver.find_element_by_class_name("s_ipt").get_attribute("class"))
print(f'3、class_name定位 获取到的元素的class属性内容:{driver.find_element_by_class_name("s_ipt").get_att
ribute("class")}')  # s_ipt
```

## link_text定位(针对a标签)
```python
# driver.find_element_by_link_text("新闻").click()
# 输出获取到的元素的文本内容
print(driver.find_element_by_link_text("新闻").text)
print(
f'4、link_text定位 获取到的元素的文本内容:{driver.find_element_by_link_text("新闻").text}')  # 新闻
```

## partial_link_text定位(针对a标签)
```python
# driver.find_element_by_partial_link_text("闻").click()
# 输出获取到的元素的文本内容
# print(driver.find_element_by_partial_link_text("闻").text)
print(f'5、partial_link_text定位 获取到的元素的文本内容:{driver.find_element_by_partial_link_text("闻").text}')  # 新闻
```


## tag_name标签名定位
```python
# 输出获取到的元素的action属性内容
# print(driver.find_element_by_tag_name("form").get_attribute("action"))
print(
    f'6、tag_name标签名定位 获取到的元素的action属性内容:{driver.find_element_by_tag_name("form").get_attribute("action")}')  # https://www.baidu.com/s
```


## xpath定位
(1)绝对路径（绝对路径使用"/"）
```python
# 举例：定位搜索框输入搜索内容"测试玉米君"
# driver.find_element_by_xpath("/html/body/div/div/div/div/div/form/span/input").send_keys("测试玉米君")
print(
    f'7.1、xpath绝对路径定位 获取到的元素的id属性内容:{driver.find_element_by_xpath("/html/body/div/div/div/div/div/form/span/input").get_attribute("id")}')  # kw
```


(2)相对路径（相对路径使用"//"）
```python
# 举例：定位搜索框输入搜索内容"测试玉米君"
# driver.find_element_by_xpath("//form/span/input").send_keys("测试玉米君")
# 输出获取到的元素的id属性内容
print(f'7.2、xpath相对路径定位 获取到的元素的id属性内容:{driver.find_element_by_xpath("//form/span/input").get_attribute("id")}')  # kw
```


(3)索引定位
索引从"1"开始，默认不填写就是"1"
```python
# 举例：定位 百度一下 按钮
# driver.find_element_by_xpath("//form/span[2]/input").click()
# 输出获取到的元素的value属性内容
print(
    f'7.3.1、xpath索引定位 取到的元素的value属性内容:{driver.find_element_by_xpath("//form/span[2]/input").get_attribute("value")}')  # 百度一下
# 举例：定位百度hao123链接
# driver.find_element_by_xpath("//div[3]/a[2]").click()
# 输出标签文本内容
print(f'7.3.2、xpath索引定位 取到的元素的文本内容:{driver.find_element_by_xpath("//div[3]/a[2]").text}')  # hao123
# 举例：定位百度hao123链接
# driver.find_element_by_xpath("//div[@id='s-top-left']/a[2]").click()
# 输出标签文本内容
print(
    '7.3.3、xpath索引定位 取到的元素的文本内容:{}'.format(driver.find_element_by_xpath('//div[@id="s-top-left"]/a[2]').text))  # hao123
```


(4)属性定位 
使用"@"符号呼叫属性
```python
# driver.find_element_by_xpath("//input[@autocomplete='off']").send_keys("测试玉米君")
print('7.4.1、xpath属性定位 取到的元素的id属性内容:{}'.format(
    driver.find_element_by_xpath("//input[@autocomplete='off']").get_attribute("id")))  # kw
# driver.find_element_by_xpath("//input[@autocomplete='off' and @name='wd']").send_keys("测试玉米君")
print('7.4.2、xpath属性定位 取到的元素的id属性内容:{}'.format(
    driver.find_element_by_xpath("//input[@autocomplete='off' and @name='wd']").get_attribute("id")))  # kw
```


(5)部分的属性值
也称为模糊方法定位
```python
# 元素属性值开头包含内容：starts-with()
# driver.find_element_by_xpath("//input[starts-with(@autocomplete,'of')]").send_keys("测试玉米君")
print('7.5.1、xpath部分的属性值定位 取到的元素的autocomplete属性内容:{}'.format(
    driver.find_element_by_xpath("//input[starts-with(@autocomplete,'of')]").get_attribute("autocomplete")))  # off
# 元素属性值结尾包含内容：substring()
# driver.find_element_by_xpath("//input[substring(@class,3)='ipt']").send_keys("测试玉米君")
print('7.5.2、xpath部分的属性值定位 取到的元素的class属性内容:{}'.format(
    driver.find_element_by_xpath("//input[substring(@class,3)='ipt']").get_attribute("class")))  # s_ipt
# 元素属性值包含内容：contains()
# driver.find_element_by_xpath("//input[contains(@class,'pt')]").send_keys("测试玉米君")
print('7.5.3、xpath部分的属性值定位 取到的元素的class属性内容:{}'.format(
    driver.find_element_by_xpath("//input[contains(@class,'pt')]").get_attribute("class")))  # s_ipt
```


(6)通过文本定位
```python
# 元素文本在xpath中可以通过text()函数获取，也可以用其来进行元素定位。
# driver.find_element_by_xpath("//a[text()='新闻']").click()
print('7.6.1、xpath文本定位 取到的元素的文本内容:{}'.format(driver.find_element_by_xpath("//a[text()='新闻']").text))  # 新闻
# driver.find_element_by_xpath("//span[text()='按图片搜索']").get_attribute("style")
print('7.6.2、xpath文本定位 取到的元素的style属性内容:{}'.format(
    driver.find_element_by_xpath("//span[text()='按图片搜索']").get_attribute("style")))  # display: none
```


(7)各种xpath组合
```python
# driver.find_element_by_xpath("//a[contains(text(),'新闻')]").click()
print('7.7.1、各种xpath组合 取到的元素的文本内容:{}'.format(driver.find_element_by_xpath("//a[contains(text(),'新闻')]").text))  # 新闻
# driver.find_element_by_xpath("//a[contains(text(),'新')]").click()
print('7.7.2、各种xpath组合 取到的元素的文本内容:{}'.format(driver.find_element_by_xpath("//a[contains(text(),'新')]").text))  # 新闻
# driver.find_element_by_xpath("//form[@id='form']/span[1]/input").send_keys("测试玉米君")
print('7.7.3、各种xpath组合 取到的元素的id属性内容:{}'.format(
    driver.find_element_by_xpath("//form[@id='form']/span[1]/input").get_attribute("id")))  # kw
```


(8)通配符*
```python
# driver.find_element_by_xpath("//*[@*='kw']").send_keys("测试玉米君")
print('7.8、xpath通配符*定位 取到的元素的id属性内容:{}'.format(
    driver.find_element_by_xpath("//*[@*='kw']").get_attribute("id")))  # kw
```


## css选择器定位
html,javascript,css,h5+css3，通过.找class，通过#找id
(1)绝对路径
```python
# driver.find_element_by_css_selector("html body div div div div div form span input").send_keys("测试玉米君")
print('8.1.1、css绝对路径定位 取到的元素的id属性内容:{}'.format(
    driver.find_element_by_css_selector("html body div div div div div form span input").get_attribute("id")))  # kw
# driver.find_element_by_css_selector("html>body>div>div>div>div>div>form>span>input").send_keys("测试玉米君")
print('8.1.2、css绝对路径定位 取到的元素的id属性内容:{}'.format(
    driver.find_element_by_css_selector("html>body>div>div>div>div>div>form>span>input").get_attribute("id")))  # kw
# driver.find_element_by_css_selector("html body div.wrapper_new div#head div.head_wrapper.s-isindex-wrap.nologin div div form span input").send_keys("测试玉米君")
print('8.1.3、css绝对路径定位 取到的元素的id属性内容:{}'.format(
    driver.find_element_by_css_selector(
        "html body div.wrapper_new div#head div.head_wrapper.s-isindex-wrap.nologin div div form span input").get_attribute(
        "id")))  # kw
```


(2)相对路径
通过class(.)和id(#)定位）可以和标签名组合使用
```python
# driver.find_element_by_css_selector("#kw").send_keys("测试玉米君")
print('8.2.1、css相对路径定位 取到的元素的id属性内容:{}'.format(
    driver.find_element_by_css_selector("#kw").get_attribute("id")))  # kw
# driver.find_element_by_css_selector(".s_ipt").send_keys("测试玉米君")
print('8.2.2、css相对路径定位 取到的元素的id属性内容:{}'.format(
    driver.find_element_by_css_selector(".s_ipt").get_attribute("id")))  # kw
# driver.find_element_by_css_selector("input#kw").send_keys("测试玉米君")
print('8.2.3、css相对路径定位 取到的元素的id属性内容:{}'.format(
    driver.find_element_by_css_selector("input#kw").get_attribute("id")))  # kw
# driver.find_element_by_css_selector("input.s_ipt").send_keys("测试玉米君")
print('8.2.4、css相对路径定位 取到的元素的id属性内容:{}'.format(
    driver.find_element_by_css_selector("input.s_ipt").get_attribute("id")))  # kw
```


(3)通过元素属性定位
```python
# 具体格式：标签名[属性="属性值"] 支持使用多个属性一起定位元素
# driver.find_element_by_css_selector("input[autocomplete='off']").send_keys("测试玉米君")
print('8.3.1、css元素属性定位 取到的元素的id属性内容:{}'.format(
    driver.find_element_by_css_selector("input[autocomplete='off']").get_attribute("id")))  # kw
# driver.find_element_by_css_selector("input[autocomplete='off'][name='wd']").send_keys("测试玉米君")
print('8.3.2、css元素属性定位 取到的元素的id属性内容:{}'.format(
    driver.find_element_by_css_selector("input[autocomplete='off'][name='wd']").get_attribute("id")))  # kw
```


(4)通过部分元素属性值（也称为模糊方法定位）

1)元素属性值开头包含内容：^=

2)元素属性值结尾包含内容：$=

3)元素属性值当中包含内容：*=

```python
# driver.find_element_by_css_selector("input[autocomplete^='of']").send_keys("测试玉米君")
print('8.4.1、css部分属性值定位 取到的元素的autocomplete属性内容:{}'.format(
    driver.find_element_by_css_selector("input[autocomplete^='of']").get_attribute("autocomplete")))  # off
# driver.find_element_by_css_selector("input[autocomplete$='ff']").send_keys("测试玉米君")
print('8.4.2、css部分属性值定位 取到的元素的autocomplete属性内容:{}'.format(
    driver.find_element_by_css_selector("input[autocomplete$='ff']").get_attribute("autocomplete")))  # off
# driver.find_element_by_css_selector("input[autocomplete*='of']").send_keys("测试玉米君")
print('8.4.3、css部分属性值定位 取到的元素的autocomplete属性内容:{}'.format(
    driver.find_element_by_css_selector("input[autocomplete*='of']").get_attribute("autocomplete")))  # off
```


(5)通过查询子元素（类似xpath中的索引的方法）

 1）子元素：A>B


 2）后代元素：A B（类似>）

 3）第一个后代元素：first-child

 4）最后一个后代元素：last-child[等同于 p:nth-last-child(1)]

 5）第n个子元素：nth-child(N)[类同:nth-of-type(N)]

 6）通过空格和>查找子元素（只能一级一级找）

```python
# driver.find_element_by_css_selector("div#s-top-left a:nth-child(1)").click()
print('8.5.1、css子元素定位 取到的元素的文本内容:{}'.format(
    driver.find_element_by_css_selector("div#s-top-left a:nth-child(1)").text))  # 新闻
# driver.find_element_by_css_selector("div#s-top-left a:first-child").click()
print('8.5.2、css子元素定位 取到的元素的文本内容:{}'.format(
    driver.find_element_by_css_selector("div#s-top-left a:first-child").text))  # 新闻
# driver.find_element_by_css_selector("div#s-top-left a:last-child").click()
print('8.5.3、css子元素定位 取到的元素的文本内容:{}'.format(
    driver.find_element_by_css_selector("div#s-top-left a:last-child").text))  #
# driver.find_element_by_css_selector("div#s-top-left a:nth-last-child(2)").click()
print('8.5.4、css子元素定位 取到的元素的文本内容:{}'.format(
    driver.find_element_by_css_selector("div#s-top-left a:nth-last-child(2)").text))  # 学术
# driver.find_element_by_css_selector("div#s-top-left a:nth-child(2)").click()
print('8.5.5、css子元素定位 取到的元素的文本内容:{}'.format(
    driver.find_element_by_css_selector("div#s-top-left a:nth-child(2)").text))  # hao123
```


(6)查找兄弟元素
1）同层级下一个元素：+

2）选择同层级多个相同标签的元素：~

 备注：

 +号可以多次使用

 ~号一般返回的是多个元素，要用find_elements接收

```python
# driver.find_element_by_css_selector("div#s-top-left a +a").click()
print('8.6.1、css子元素定位 取到的元素的文本内容:{}'.format(
    driver.find_element_by_css_selector("div#s-top-left a +a").text))  # hao123
# driver.find_element_by_css_selector("div#u1 a +a +a").click()
print('8.6.2、css子元素定位 取到的元素的文本内容:{}'.format(
    driver.find_element_by_css_selector("div#s-top-left a +a +a").text))  # 地图
```


# 自动化框架中封装定位
```python
from selenium.webdriver.common.by import By

driver.find_element(By.ID, "kw").send_keys("测试玉米君")
```


# 总结
**定位元素的方式有8种，写法有两种**
## id定位
```python
driver.find_element_by_id("kw")
driver.find_element(By.ID, "kw")
```


## name定位
```python
driver.find_element_by_name("wd")
driver.find_element(By.NAME, "wd")
```


## class定位
```python
driver.find_element_by_class_name("s_ipt")
driver.find_element(By.CLASS_NAME, "s_ipt")
```


## tag_name定位
```python
driver.find_element_by_tag_name("form")
driver.find_element(By.TAG_NAME, "form")
```


## link_text定位
```python
driver.find_element_by_link_text("新闻")
driver.find_element(By.LINK_TEXT, "新闻")
```


## partial_link_text定位
```python
driver.find_element_by_partial_link_text("新")
driver.find_element(By.PARTIAL_LINK_TEXT, "新")
```


## XPath定位
```python
driver.find_element_by_xpath("//input[@id='kw']")
driver.find_element(By.XPATH, "//input[@id='kw']")
```


## CSS定位
```python
driver.find_element_by_css_selector("#kw")
driver.find_element(By.CSS_SELECTOR, "#kw")
```

*****
欢迎来跟博主讨论自动化有关的问题。