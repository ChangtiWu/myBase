# Python爬虫

# 1 Selenium+chromedriver模拟浏览器

## 1.1 准备工作

安装selenium

```bash
conda install selenium
```

下载chromedriver.exe，下载地址：https://sites.google.com/chromium.org/driver/downloads，根据自己的chrome版本下载相应的驱动引擎，为路径方便，放到爬虫py文件的同一目录下。

## 1.2 开始

首先，引入selenium.webdriver与ChromeOptions

```python
from selenium import webdriver
from selenium.webdriver import ChromeOptions
```

配置参数

```python
options = ChromeOptions()
options.add_argument('--headless') #隐藏浏览器，若注释掉则显示浏览器
options.add_argument('--disable-gpu')
driver = webdriver.Chrome(executable_path='./chromedriver.exe', options=options)#chromedriver.exe放在同一目录下
```

定义要访问的初始页面

```python
url = 'https://weibo.com/'
```

请求页面

```python
driver.get(url)
```

## 1.3 定位元素

此处定位均使用的百度首页输入框。

```python
#通过标签属性Id查找元素
方法：find_element_by_id(element_id)
实例：driver.find_element_by_id("kw")

#通过标签属性name查找元素
方法：find_element_by_name(element_name)
实例：driver.find_element_by_name("wd")

#通过标签Xpath路径查找元素
方法：find_element_by_xpath(xpath)
实例：driver.find_element_by_xpath("//*[@id="kw"]")

#通过标签名tagname查找元素
方法：find_element_by_tag_name(tag_name)
实例：driver.find_element_by_tag_name("input")
注意：通过tag_name查找时使用find_element_by_tag_name查找到的是第一个标签的tag_name

#通过标签中的元素文本链接查找元素
方法：find_element_by_link_text(link_text)
实例：driver.find_element_by_link_text('百度一下')

#通过标签的class属性查找元素
方法：find_elements_by_class_name(class_name)
实例：driver.find_elements_by_class_name("s_ipt")

#通过css样式查找元素
方法：find_element_by_css_selector()
实例：driver.find_element_by_css_selector("#kw")

#根据cookie name 查找
方法：driver.get_cookie(cookie_name)
实例：driver.get_cookie("NET_SessionId")
```

## 1.4 对定位的元素进行操作

```python
#点击操作
方法：click()
实例：driver.find_element_by_id("kw").click()

#获取元素坐标
方法：location
解释：首先查找到你要获取元素的，然后调用location方法
实例：driver.find_element_by_id("kw").location

#表单的提交
方法：submit
解释:查找到表单（from）直接调用submit即可
实例：driver.find_element_by_id("su").submit()

#获取CSS的属性值
方法：value_of_css_property(css_name)
实例：driver.find_element_by_id("su").value_of_css_property("color")

#获取元素的属性值
方法：get_attribute(element_name)
实例：driver.find_element_by_id("kw").get_attribute("type")

#判断元素是否被选中
方法：is_selected()
实例：driver.find_element_by_id("form1").is_selected()

#返回元素的大小
方法：size
实例：driver.find_element_by_id("kw").size
返回值：{'width': 102, 'height': 38}

#判断元素是否显示
方法：is_displayed()
实例：driver.find_element_by_id("kw").is_displayed()

#判断元素是否被使用
方法：is_enabled()
实例：driver.find_element_by_id("kw").is_enabled()

#获取元素的文本值
方法：text
实例：driver.find_element_by_class_name("mnav").text

#输入值
方法：send_keys(*values)
实例：driver.find_element_by_id("kw").send_keys('admin')
注意如果是中文需要加u
driver.find_element_by_id("kw").send_keys(u'青春')

#返回元素的tagName
方法：tag_name
实例：driver.find_element_by_id("kw").tag_name
```

## 1.5 其他操作

```python
#向前
方法：forward()
实例：driver.forward()

#返回上一页
方法：back()
实例：driver.back()

#返回当前会话中的cookies
方法：get_cookies()
实例：driver.get_cookies()

#删除浏览器所有的cookies
方法：delete_all_cookies()
实例：driver.delete_all_cookies()

#删除指定的cookie
方法：delete_cookie(name)
实例：deriver.delete_cookie("my_cookie_name")

#截取当前页面
方法：get_screenshot_as_file(filename)
实例：driver.get_screenshot_as_file(r"C:\Users\Eric\Desktop\test.png")

#获取当前窗口的坐标
方法：get_window_position()
实例：driver.get_window_position()

#获取当前窗口的长和宽
方法：get_window_size()
实例：driver.get_window_size()

#获取当前页面的Url函数
方法：current_url
实例：driver.current_url

#关闭浏览器
方法：close()
实例：driver.close()

#关闭浏览器并且推出驱动程序
方法：quit()
实例：driver.quit()

#浏览器窗口最大化
方法：maximize_window()
实例：driver.maximize_window()

#查看浏览器的名字
方法：name
实例：drvier.name

#刷新当前浏览器
方法：refresh
实例：drvier.refresh()
```

## 1.6 等待操作

### 1.6.1 显示等待

https://blog.csdn.net/sinat_41774836/article/details/88965281

### 1.6.2 隐式等待

设置隐式等待时间，当查找元素或元素并没有立即出现的时候，隐式等待将等待一段时间再查找DOM。一旦设置了隐式等待，则它存在整个WebDriver对象实例的声明周期中，它将会在寻找每个元素的时候都进行等待。

```python
driver.implicitly_wait(10) #单位为s，默认为0
```

### 1.6.3 强制等待

设置程序休眠。

```python
import time
time.sleep(10) #单位为s
```

## 1.7 用cookies登录网页

首先写一个获取网站cookies的py文件，将网站cookies保存成txt。在程序里设置一个等待时间（40s），然后在这空挡时间里手动登录目标网站，等空挡时间过去程序接着就获取刚刚登陆的cookies。

```python
from selenium import webdriver
import time
import json

#填写webdriver的保存目录
driver = webdriver.Chrome('./chromedriver.exe')

#记得写完整的url 包括http和https
driver.get('https://weibo.com/')

#程序打开网页后40秒内手动登陆账户
time.sleep(40)

with open('cookies.txt','w') as cookief:
    #将cookies保存为json格式
    cookief.write(json.dumps(driver.get_cookies()))

driver.close()
driver.quit()
```

下次采用cookies.txt用cookies登录目标网页。cookies里有一项expiry，会报错，有两种解决办法：

1. 将expiry类型变为int（其实不太清楚为什么变为int就可以）。
2. 删除该字段。

```python
#首先清除由于浏览器打开已有的cookies
driver.delete_all_cookies()

with open('cookies.txt','r') as cookief:
    #使用json读取cookies 注意读取的是文件 所以用load而不是loads
    cookieslist = json.load(cookief)

    # 方法1 将expiry类型变为int
    for cookie in cookieslist:
        #并不是所有cookie都含有expiry 所以要用dict的get方法来获取
        if isinstance(cookie.get('expiry'), float):
            cookie['expiry'] = int(cookie['expiry'])
        driver.add_cookie(cookie)

    #方法2删除该字段
    # for cookie in cookieslist:
    #     #该字段有问题所以删除就可以  浏览器打开后记得刷新页面 有的网页注入cookie后仍需要刷新一下
    #     if 'expiry' in cookie:
    #         del cookie['expiry']
    #     driver.add_cookie(cookie)

driver.refresh()    # 刷新后页面显示已登录
```

