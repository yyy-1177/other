# 实验02
## 第五题
```Python
import turtle  

#创建画布和画笔
screen = turtle.Screen()
screen.title("四瓣花图")
t = turtle.Turtle()
t.speed(5) #设置画笔速度

#绘制花
for _ in range(4):
	t.circle(100, 180) #绘制半圆
	t.left(90) #调整方向，逆时针绘制

#隐藏画笔并结束
t.hideturtle()
screen.mainloop()
```
## 第六题
```Python
import turtle

#创建画布和画笔
screen = turtle.Screen()
screen.title("嵌套六角形")
t = turtle.Turtle()
t.speed(5) #设置画笔速度

#初始边长和递增长度
side_length = 1
increment = 3

#绘制嵌套六角形
for _ in range(60): #控制边数（6边为一组）
	t.forward(side_length) #绘制边
	t.left(60) #六边形内角120°，转动60°为下一边
	side_length += increment #增加边长

# 隐藏画笔并结束
t.hideturtle()
screen.mainloop()
```
# 实验03
## 第一题
### 递归
```Python
#递归
def fact_recursive(n):
	if n == 0 or n == 1: #0!和1!都是1
		return 1
	else:
		return n * fact_recursive(n - 1)

#测试递归实现
n = int(input("请输入一个正整数："))
if n >= 0:
	print(f"{n}! = {fact_recursive(n)}")
else:
	print("请输入一个非负整数！")
```
### 非递归
```Python
#非递归
def fact_iterative(n):
	result = 1
	for i in range(1, n + 1):
		result *= i
	return result
n = int(input("请输入一个正整数："))
if n >= 0:
	print(f"{n}! = {fact_iterative(n)}")
else:
	print("请输入一个非负整数！")
```
## 第二题
- 这道题我不太清楚他表达的是什么，于是我按照不同的想法写了两个不一样的
- 第一个输入数字是可以随时停，没有限制
- 第二个是通过更改代码来限制输入的个数
- 因为第一个是会跳出来多一行字，感觉不是他需要的
- 我不太清楚这道题的需求，你看看需要哪一个，如果两个都不行的话再找我
### 方案1
```Python
def min_n(a, b, *c):
	return min(a, b, *c)

#main
print("请逐行输入数字，每次输入一个数，按回车结束当前输入。")
print("当输入为空时结束输入并计算最小值。")

numbers = [] #用于存储用户输入的数字
counter = 1 #用于显示 n1和n2 等编号
min_first_two = None #用于保存n1和n2的最小值

while True:
	user_input = input(f"请输入一个整数n{counter}（或按回车结束）：")
	if user_input == "": #如果输入为空，结束输入
		break
	try:
		number = int(user_input) #将输入转换为数字
		numbers.append(number) #添加到列表中

#仅在输入n1和n2时，记录n1和n2的最小值
		if counter == 2:
			min_first_two = min(numbers[0], numbers[1])
		counter += 1 #增加编号
	except ValueError:
		print("输入无效，请输入一个数字！")

#检查输入数量是否足够
if len(numbers) < 2:
	print("请至少输入两个数值！")
else:
#输出n1和n2的最小值和所有数的最小值
	num_labels = ", ".join([f"n{i+1}" for i in range(len(numbers))]) #生成 n1, n2, ... 格式
	print(f"n1和n2的最小值为 {min_first_two}")
	print(f"{num_labels} 的最小值为：{min_n(numbers[0], numbers[1], *numbers[2:])}")
```
### 方案2
```Python
def min_n(a, b, *c):
	return min(a, b, *c)

#main
n = 5 #设定输入的整数数量
print(f"请输入 {n} 个整数：")

numbers = [] #用于存储用户输入的数字

for i in range(1, n+1): #输入固定数量的数字
	while True:
		try:
			user_input = int(input(f"请输入一个整数n{i}："))
			numbers.append(user_input) #添加到列表中
			break #输入成功，跳出循环
		except ValueError:
			print("输入无效，请输入一个整数！")

#检查输入数量是否足够
if len(numbers) < 2:
	print("请至少输入两个数值！")
else:
#输出n1和n2的最小值和所有数的最小值
	num_labels = ", ".join([f"n{i+1}" for i in range(len(numbers))]) #生成 n1, n2, ... 格式
	print(f"n1和n2的最小值为：{min(numbers[0], numbers[1])}")
	print(f"{num_labels} 的最小值为：{min_n(numbers[0], numbers[1], *numbers[2:])}")
```
## 第三题
```Python
def fib(n):
	if n == 0 or n == 1:
		return 1
	else:
		return fib(n - 1) + fib(n - 2)

#输出前 20 项
print("斐波那契数列前 20 项：")

#使用格式化输出，每个数宽度为 5，右对齐(美观)
for i in range(20):
	print(f"{fib(i):5}", end="")
	if (i + 1) % 10 == 0:
		print() #每10个数换行(美观)
```
## 第四题
```Python
import turtle 

def draw_inverted_triangle(rows):
#设置画布
	screen = turtle.Screen()
	screen.setup(width=600, height=600)

#创建一个turtle对象
	t = turtle.Turtle()
	t.speed("fastest") #设置绘图速度为最快

#圆圈的大小（直径）
	circle_diameter = 40

#当前x和y坐标
	y = rows * circle_diameter // 2

#从顶部开始
	for i in range(rows):

#计算当前行的圆圈数量
		num_circles = rows - i

#计算当前行的x偏移量（用于居中）
		x_offset = -(num_circles * circle_diameter // 2) + circle_diameter // 2

#绘制当前行的圆圈
		for j in range(num_circles):
			t.penup()
			t.goto(x_offset + j * circle_diameter, y)
			t.dot(circle_diameter,"blue") #绘制填充的圆圈(蓝色)
#更新y坐标以绘制下一行
		y -= circle_diameter
#隐藏turtle并显示窗口
	t.hideturtle()
	screen.mainloop()

#获取用户输入的行数
try:
	rows = int(input("请输入需要绘制的行数（填充圆圈组成的倒三角形）："))
	draw_inverted_triangle(rows)
except ValueError:
	print("请输入一个有效的整数！")
```