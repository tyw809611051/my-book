#### 形式
```
if condition_1:
    statement_block_1
elif condition_2:
    statement_block_2
else:
    statement_block_3
```

**示例:**
```
age = int(input("Age of the dog: "))
print()
if age < 0:
	print("This can hardly be true!")
elif age == 1:
	print("about 14 human years")
elif age == 2:
	print("about 22 human years")
elif age > 2:
	human = 22 + (age -2)*5
	print("Human years: ", human)

### 
input('press Return>')
```

**注意：**
1. 每个条件后面要使用冒号（:），表示接下来是满足条件后要执行的语句块。
2. 使用缩进来划分语句块，相同缩进数的语句在一起组成一个语句块。
3. 在Python中没有switch – case语句。