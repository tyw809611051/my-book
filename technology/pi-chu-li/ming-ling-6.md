### 运算符
- 算术运算符
- 关系运算符
- 逻辑运算符
- 赋值运算符


#### 算术运算符
|运算符|描述|
|---|---|
|+|相加|
|-	|相减|
|*|相乘|
|/	|相除|
|%|取模|

#### 关系运算符
|运算符|描述|
|---|---|
|EQU	|测试两个对象之间的相等性	|
|NEQ	|测试两个对象之间的不相等性|
|LSS	|检查左对象是否小于右操作数|
|LEQ	|检查左对象是否小于或等于右操作数|
|GTR	|检查左对象是否大于右操作数|
|GEQ	|检查左对象是否大于或等于右操作数|

#### 逻辑运算符
> AND，OR，XOR，但只适用于二进制数字,唯一用于条件运算的是NOT

|运算符|描述|
|---|---|
|AND|	这是逻辑的“和”运算符|
|OR|	这是逻辑“或”运算符|
|NOT|	这是逻辑的“非”运算符|

#### 赋值运算符
|运算符|描述|示例|
|---|---|---|
|+=|	这将右操作数相加到左操作数，并将结果分配给左操作数|	Set /A a = 5; a += 3，结果为：8|
|-=	|从左操作数中减去右操作数，并将结果赋给左操作数。|	Set /A a = 5; a -= 3，结果为：8|
|*=	|将右操作数与左操作数相乘，并将结果赋给左操作数。|	Set /A a = 5; a *= 3，结果为：15|
|/=	|将左操作数除以右操作数，并将结果赋给左操作数。	|Set /A a = 6; a/ = 3，结果为：15|
|%=	|将两个操作数取模，并将结果赋给左操作数|