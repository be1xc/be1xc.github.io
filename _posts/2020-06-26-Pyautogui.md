---
title:      Pyautogui
date:       2020-06-26
tags:  Python     
---


## Pyautogui



#### 常用

````python
import pyautogui

# 启用防故障功能, 鼠标强制移动到屏幕左上脚(0,0), 直接抛出 failSafeException 异常
pyautogui.FAILSAFE = True

# 判断坐标是否在屏幕上
x , y = 122 , 200
puautogui.onScreen(x,y)  #结果为 True

# 获取运行环境屏幕尺度
width, height = pyautogui.size()
````



#### 鼠标

````python
import pyautogui

X,Y = pyautogui.position() # 获取鼠标当前坐标

# 鼠标移动
## 绝对移动
pyautogui.moveTo(x,y,duration=1)  # duration 为移动时间 单位秒
## 相对当前位置移动
pyautogui.moveRel(x,y,duration=1) # 向当前位置 右移X 下移Y 像素 (可以为负数)

# 拖拽
pyautogui.dragTo(x,y(,sec),button='left') # 按住左键拖拽到x,y  sec为持续时间(s)
pyautogui.dragRel(x,y(,sec),button='left') # 按住左键往右X 下Y 拖拽像素

# 点击
pyautogui.click()  # 当前位置点击
pyautogui.click(x,y)  # 在 x,y 位置点击
pyautogui.click(x,y,duration=1) # 1秒时间移动到x,y并点击
pyautogui.doubleClick() # 当前位置双击 和click 一样可以设置参数
pyautogui.tripleClick() # 三击 同上
pyautogui.mouseDown() # 鼠标左键按下
pyautogui.mouseUp()  # 左键松开
pyautogui.mouseDown(button='right') # 按下鼠标右键
pyautogui.mouseUp(button='right', x=100, y=200) # 移动到(100, 200)位置，然后松开鼠标右键

# 滑轮
## scroll函数控制鼠标滚轮的滚动，amount_to_scroll参数表示滚动的格数。正数则页面向上滚动，负数则向下滚动
## pyautogui.scroll(clicks=amount_to_scroll, x=moveToX, y=moveToY)
pyautogui.scroll(10) # 向上滚动10格
pyautogui.scroll(-10) # 向下滚动10格
pyautogui.scroll(10, x=100, y=100) # 移动到(100, 100)位置再向上滚动10格

# 渐变函数 可以用于moveTo()，moveRel()，dragTo()和dragRel()函数
#  开始很慢，不断加速
pyautogui.moveTo(100, 100, 2, pyautogui.easeInQuad)
#  开始很快，不断减速
pyautogui.moveTo(100, 100, 2, pyautogui.easeOutQuad)
#  开始和结束都快，中间比较慢
pyautogui.moveTo(100, 100, 2, pyautogui.easeInOutQuad)
#  一步一徘徊前进
pyautogui.moveTo(100, 100, 2, pyautogui.easeInBounce)
#  徘徊幅度更大，甚至超过起点和终点
pyautogui.moveTo(100, 100, 2, pyautogui.easeInElastic)
````



#### 键盘

````python
import pyautogui

pyautogui.typewrite('type here'(,interval=0.25)) # 输入字符串 interval使每次键入间隔秒数
pyautogui.press('enter') # 按一次enter
pyautogui.press(['right','left','left'])  # 顺序完成每一个键位的敲击
pyautogui.keyDown('shift') # 按下 shift 键
pyautogui.keyUp('shift')  # 松开 shift 键

pyautogui.keyDown('shift')
pyautogui.press('4')
pyautogui.keyUp('shift') # 输出 $ 符号的按键

pyautogui.hotkey('ctrl', 'v') # 组合按键（Ctrl+V）

pyautogui.KEYBOARD_KEYS # 显示press()，keyDown()，keyUp()和hotkey()函数可以输入的按键名称
````



#### 弹窗

````python
import pyautogui

# 显示一个简单的带文字和OK按钮的消息弹窗。用户点击后返回button的文字。
pyautogui.alert(text='', title='', button='OK')
b = pyautogui.alert(text='要开始程序么？', title='请求框', button='OK')
print(b) # 输出结果为OK
 
# 显示一个简单的带文字、OK和Cancel按钮的消息弹窗，用户点击后返回被点击button的文字，支持自定义数字、文字的列表。
pyautogui.confirm(text='', title='', buttons=['OK', 'Cancel']) # OK和Cancel按钮的消息弹窗
pyautogui.confirm(text='', title='', buttons=range(10)) # 10个按键0-9的消息弹窗
a = pyautogui.confirm(text='', title='', buttons=range(10))
print(a) # 输出结果为你选的数字
 
# 可以输入的消息弹窗，带OK和Cancel按钮。用户点击OK按钮返回输入的文字，点击Cancel按钮返回None。
pyautogui.prompt(text='', title='', default='')
 
# 样式同prompt()，用于输入密码，消息用*表示。带OK和Cancel按钮。用户点击OK按钮返回输入的文字，点击Cancel按钮返回None。
pyautogui.password(text='', title='', default='', mask='*')
````



#### 图像

````python
import pyautogui

pyautogui.screenshot(r'C:\Users\ZDH\Desktop\PY\my_screenshot.png') # 截全屏并设置保存图片的位置和名称
im = pyautogui.screenshot(r'C:\Users\ZDH\Desktop\PY\my_screenshot.png') # 截全屏并设置保存图片的位置和名称
print(im) # 打印图片的属性
 
# 不截全屏，截取区域图片。截取区域region参数为：左上角XY坐标值、宽度和高度
pyautogui.screenshot(r'C:\Users\ZDH\Desktop\PY\region_screenshot.png', region=(0, 0, 300, 400))
 
pix = pyautogui.screenshot().getpixel((220, 200)) # 获取坐标(220,200)所在屏幕点的RGB颜色
positionStr = ' RGB:(' + str(pix[0]).rjust(3) + ',' + str(pix[1]).rjust(3) + ',' + str(pix[2]).rjust(3) + ')'
print(positionStr) # 打印结果为RGB:( 60, 63, 65)
pix = pyautogui.pixel(220, 200) # 获取坐标(220,200)所在屏幕点的RGB颜色与上面三行代码作用一样
positionStr = ' RGB:(' + str(pix[0]).rjust(3) + ',' + str(pix[1]).rjust(3) + ',' + str(pix[2]).rjust(3) + ')'
print(positionStr) # 打印结果为RGB:( 60, 63, 65)
 
# 如果你只是要检验一下指定位置的像素值，可以用pixelMatchesColor(x,y,RGB)函数，把X、Y和RGB元组值穿入即可
# 如果所在屏幕中(x,y)点的实际RGB三色与函数中的RGB一样就会返回True，否则返回False
# tolerance参数可以指定红、绿、蓝3种颜色误差范围
pyautogui.pixelMatchesColor(100, 200, (255, 255, 255))
pyautogui.pixelMatchesColor(100, 200, (255, 255, 245), tolerance=10)
 
# 获得文件图片在现在的屏幕上面的坐标，返回的是一个元组(top, left, width, height)
# 如果截图没找到，pyautogui.locateOnScreen()函数返回None
a = pyautogui.locateOnScreen(r'C:\Users\ZDH\Desktop\PY\region_screenshot.png')
print(a) # 打印结果为Box(left=0, top=0, width=300, height=400)
x, y = pyautogui.center(a) # 获得文件图片在现在的屏幕上面的中心坐标
print(x, y) # 打印结果为150 200
x, y = pyautogui.locateCenterOnScreen(r'C:\Users\ZDH\Desktop\PY\region_screenshot.png') # 这步与上面的四行代码作用一样
print(x, y) # 打印结果为150 200
 
# 匹配屏幕所有与目标图片的对象，可以用for循环和list()输出
pyautogui.locateAllOnScreen(r'C:\Users\ZDH\Desktop\PY\region_screenshot.png')
for pos in pyautogui.locateAllOnScreen(r'C:\Users\ZDH\Desktop\PY\region_screenshot.png'):
  print(pos)
# 打印结果为Box(left=0, top=0, width=300, height=400)
a = list(pyautogui.locateAllOnScreen(r'C:\Users\ZDH\Desktop\PY\region_screenshot.png'))
print(a) # 打印结果为[Box(left=0, top=0, width=300, height=400)]
````

