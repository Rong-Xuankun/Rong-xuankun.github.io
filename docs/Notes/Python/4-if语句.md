# if语句

## 5.1 一个简单示例

```py
cars = ['audi', 'bmw', 'subaru', 'toyota']

for car in cars:
    if car == 'bmw':
        print(car.upper())
    else:
        print(car.title())
```

```py
Audi
BMW
Subaru
Toyota
```

-----

## 5.2 条件测试

每个if语句的核心都是一个值为True或False的表达式，这种表达式被称为`条件测试`。

### 5.2.1 检查是否相等

```py
>>> car = 'bmw'
>>> car == 'bmw'
    True
```

```py
>>> car = 'audi'
>>> car == 'bmw'
    False
```

### 5.2.2 检查是否相等时不考虑大小写

在Python中检查是否相等时区分大小写：

```py
>>> car = 'Audi'
>>> car =='audi'
    False
```

如果大小写很重要，这种行为有其优点。但如果大小写无关紧要，而只想检查变量的值，可以将变量的值转换为小写，再进行比较：

```py
>>> car = 'Audi'
>>> car.lower() == 'audi'
    Ture
```

### 5.2.3 检查是否不相等

要判断两个值是否不等，可使用`!=`。

```py
requested_topping = 'mushrooms'

if requested_topping != 'anchovies':
    print("Hold the anchovies!")
```

```py
Hold the anchovies!
```

有时候检查两个值是否不等的效率更高。

### 5.2.4 比较数字

条件语句中可以包含各种数字比较，如小于、小于等于、大于、大于等于：

```py
>>> age = 19
>>> age < 21
    True
>>> age <= 21
    True
>>> age > 21
    False
>>> age >= 21
    False
```

### 5.2.5 检查多个条件

* 使用`and`来检查多个条件

```py
>>> age_0 = 22
>>> age_1 = 18
>>> age_0 >= 21 and age_1 >= 21
    False
>>> age_1 = 22
>>> age_0 >= 21 and age_1 >= 21
    True
```

为改善可读性，可以将每个测试都分别放在一对括号里，但并非必须要这样做：

```py
(age_0 >= 21) and (age_1 >= 21)
```

* 使用`or`来检查多个条件

```py
>>> age_0 = 22
>>> age_1 = 18
>>> age_0 >= 21 or age_1 >= 21
    True
>>> age_0 = 18
>>> age_0 >= 21 or age_1 >= 21
    False
```

### 5.2.6 检查特定值是否包含在列表中

要判断特定的值是否已包含在列表中，可使用关键字`in`。

```py
>>> requested_topping = ['mushrooms', 'onions', 'pineapple']
>>> 'mushrooms' in requested_toppings
    True
>>> 'pepperoni' in requested_toppings
    False
```

### 5.2.7 检查特定值是否不包含在列表中

可使用关键字`not in`：

```py
banned_users = ['andrew', 'carolina', 'david']
user = 'marie'

if user not in banned_users:
    print(user.title() + ", you can post a response if you wish.")
```

```py
Marie, you can post a response if you wish.
```

### 5.2.8 布尔表达式

```py
game_active = True
can_edit = False
```

布尔表达式的结果要么为`True`， 要么为`False`。

-----

## 5.3 if语句

### 5.3.1 简单的if语句

### 5.3.2 if-else语句

```py
age = 17
if age >= 18:
    print("You are old enough to vote!")
    print("Have you registered tp vote yet?")
else:
    print("Sorry, you are too young to vote.")
    print("Please register to vote as soon as you turn 18!")
```

### 5.3.3 if-elif-else语句

```py
age = 12

if age < 4:
    print("Your admission cost is $0.")
elif age < 18:
    print("Your admission cost is $5.")
else:
    print("Your admission cost is $10.")
```

为了使代码更加简洁：

```py
age = 12

if age < 4:
    price = 0
elif age < 18:
    price = 5
else:
    price = 10

print("Your admission cost id $" + str(price) + ".")
```

### 5.3.4 使用多个elif代码块

### 5.3.5 省略else代码块

### 5.3.6 测试多个条件

-----

## 5.4 使用if语句处理列表

### 5.4.1 检查特殊元素

```py
requested_toppings = ['mushrooms', 'green peppers', 'extra cheese']

for requested_topping in requested_toppings:
    print("Adding " + requested_topping + ".")

print("\nFinished making your pizza!")
```

```py
Adding mushrooms.
Adding green peppers.
Adding extra cheese.

Finished making your pizza!
```

```py
requested_toppings = ['mushrooms', 'green peppers', 'extra cheese']

for requested_topping in requested_toppings:
    if requested_topping == 'green peppers':
        print("Sorry, we are out of green peppers right now.")
    else:
        print("Adding " + requested_topping + ".")

print("\nFinished making your pizza!")
```

```py
Adding mushrooms.
Sorry, we are out of green peppers right now.
Adding extra cheese.

Finished making your pizza!
```

### 5.4.2 确定列表不是空的

```py
requested_toppings = []

if requested_toppings:
    for requested_topping in requested_toppings:
        print("Adding " + requested_topping + ".")
    print("\nFinished making your pizza!")
else:
    print("Are you sure you want a plain pizza?")
```

```py
Are you sure you want a plain pizza?
```

### 5.4.3 使用多个列表

```py
available_toppings = ['mushrooms', 'olives', 'green peppers', 'pepperoni', 'pineapple', 'extra cheese']

requested_toppings = ['mushrooms', 'french fries', 'extra cheese']

for requested_topping in requested_toppings:
    if requested_topping in available_toppings:
        print("Adding " + requested_topping + ".")
    else:
        print("Sorry, we don't have " + requested_topping + ".")

print("\nFinished making your pizza!")
```

```py
Adding mushrooms.
Sorry, we don't have french fries.
Adding extra cheese.

Finished making your pizza!
```

-----

## 5.6 小结

在本章中，你学习了如何编写结果要么为True要么为False的条件测试。你学习了如何编写简单示if语句、if-else语句和if-elif-else结构。在程序中，你使用了这些结构来测试特定的条件，以确定这些条件是否满足。你学习了如何在利用高效的for循环的同时，以不同于其他元素的方式对特定的列表元素进行处理。