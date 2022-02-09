# 运算符
## 1. 算数运算符
![](attachments/Pasted%20image%2020220102222845.png)
除法默认结果是整数，因为表达式的最终结果由表达式的最高类型决定，整数默认为int型，除法表达式的结果也是int整数，含有小数的结果自动舍弃小数部分。

```java
int a =10;  
int b =3;  
System.out.println(a+b);//13  
System.out.println(a-b);//7  
System.out.println(a*b);//30  
System.out.println(a/b);//3-----因为3.3333自动转换为3

```

```ad-n
表达式先进行强制类型转换，后计算
```

```java
int a =10;  
int b =3;
float c = (float)a/b;//3.3333333333333335 假如是先运算，会得到3，转float变为3.0,但实际结果是3.3333证明先强转，后计算
double rs = a/b;  
System.out.println(rs);//3.0----因为表达式结果是3
```
这里发生的过程是
 float c = (float) b / a;
首先，因为a，b都是int类型，因此在开始前，会先把b的值进行==强制类型转化==为float类型的值(b的数据类型不会变，只是临时另外创建了一个float类型的值)，然后在计算前，这时候，分子是float类型 ，分母是int类型，所以又==自动类型转换==，并且由低转高，分母也被强制类型转为float类型了。因此最终的输出结果是3.3333333.（因为在计算中，不同类型的数据先转化为同一类型，然后才进行运算。）

相同的，如果是 float c = b / (float) a; 这时候呢？是先计算还是先强制类型转换？结论也是一样的，只不过这次是先强制类型转换的是a的值罢了。




>或者通过改表达式来得到含小数的结果,注意运算顺序

```java
System.out.println(a*1.0/b);//3.3333333333333335因为a先和1.0运算，自动类型转换 ， 小转换为大

System.out.println(a/b*1.0);//3.0 因为a/b先运算完了得到3然后和1.0运算
```



>案例
```java
拆分三位数，分别输出个位十位百位  
 int data = 123;  
 // 个位：123 /10 取余  
 System.out.println(data % 10);//商12余3  
 //十位 123/10 %10 取余  
 System.out.println(data /10 % 10); //123/10==12, 12/10 商1余2  
 //百位  
 System.out.println(data/100); // 整数除法保留整数

```


## 2. 加号作连接符
“+” 与==字符串==运算的时候，做连接符，结果仍是==字符串==

```ad-n
能算则算，不能算则在一起
```
>能算则算时注意与单个字符运算时遵循ASCII码表


```java
int a = 5;  
System.out.println("abc"+ "a");//abca  
System.out.println("abc"+ a);//abc5  
System.out.println(5 + a);//10  
System.out.println("abc"+5 + 'a');//abc5a  
System.out.println("abc"+5 + a);//abc55  
System.out.println(5+"abc"+5 );//5abc5  
System.out.println('a'+ a);//102 单个字符是用ASCII码a=97  
System.out.println("a"+ a);//a5 字符串引号做字符串处理，不能用ASCII  
System.out.println('a'+ "" + a);//a5 中间没有空格，'a'和""运算得到的是字符串"a"+a  
System.out.println( a+ 'a' +"abc");//错5aabc---对102abc  
System.out.println( "abc"+ a+ 'a');//abc5a  
System.out.println( "abc"+ (a+ 'a'));//错abc10----对abc102
```

## 3. 自增自减

<!--哈哈我是注释，不会在浏览器中显示。

表头|表头|表头
---|:--:|---:
内容|内容|内容
内容|内容|内容

第二行分割表头和内容。
- 有一个就行，为了对齐，多加了几个
文字默认居左
-两边加：表示文字居中
-右边加：表示文字居右
注：原生的语法两边都要用 | 包起来。此处省略

-->

符号|作用|说明|
:--:|:--:|:--:
++|自增|变量自身的值加一
--|自减|变量自身的值减一

>++ 和 -- ==单独使用时==既可以放在变量前面也可以放在变量后面 a++; 和++a;等同
>++ -- 只能操作变量，不能操作字面量

>注意，++--如果不是单独使用（放在表达式里，或同时由其他操作），放在变量前后会由明显区别

```ad-n
放在变量前----前置自增自减运算符----运算前进行自增自减
int a = 10;
int rs = ++a;// a = a+1,rs=a, rs = 11, a=11
```
```ad-n
放在变量后----后置自增自减运算符----用后进行自增自减，==注意！！某一部分用过变量的值之后立马进行自增自减，不要等整个表达式都计算完！==
int a = 10;
int rs = a++;// rs = a, a = a+1; rs = 10, a=11
```

>案例

```
int c = 10;  
int d = 5;  
int rs3 = c++ + ++c - --d - ++d +1 + c--;  
System. out. println(rs3);  //26
System. out. println(c);  //11
System. out. println(d);  //5
  
/* 方法：创建3行变量，随着变化更改变量值  
c 10--11--12--/--/--11  
d 5--/--/4---5  
rs 10+ (11+1)-4-5+1+12 = 26  
*/

```


## 4. 扩展赋值运算符
![](attachments/Pasted%20image%2020220103143705.png)

先运算后赋值

```java
int a = 10;  
int b = 200;  
a+=b; //a = (int) a+b;  
System.out.println(a);//210

```

隐含对结果整体进行强制类型转换，数据类型同加号左边的变量
![](attachments/Pasted%20image%2020220103144503.png)

```java
package basic;  
  
public class operator {
public static void main(String[] args) {
byte i = 11;  
 byte j = 22;  
//        i = i+j; //当操作数是byte,short,char时,会自动转化为int类型;返回结果为int。  
 i+=j;// 但是i+=j;是可以的因为i = (byte)(i+j); 强制转换的类型和i相同
 System.out.println(i);//33
System.out.println(getType(i));  
}  

//查看数据类型的方法
private static String getType(Object a) {  
    return a.getClass().toString();  
}
}

##结果
//33
//class java.lang.Byte

```

## 5. 关系运算符
对数据进行条件判断的符号，返回值为true or false 的布尔值。
![](attachments/Pasted%20image%2020220103152727.png)

```java
int a =10;  
int b =10;  
boolean rs = a==b;  
boolean rs2 = a>b;  
System.out.println(rs);//true  
System.out.println(rs2);//false
```


## 6. 逻辑运算符
可以把多个条件的布尔结果放在一起运算，最终返回一个布尔结果；
![](attachments/Pasted%20image%2020220103153657.png)

异或：如果a、b两个值不相同，则异或结果为1(true)。如果a、b两个值相同，异或结果为0(false)。

异或也叫半加运算，其运算法则相当于不带进位的二进制加法：二进制下用1表示真，0表示假
0⊕0=0，1⊕0=1，0⊕1=1，1⊕1=0（同为0，异为1）



### 短路逻辑运算符
运算结果一样，但是通过左边能判断出最终布尔值的时候，右边不执行
![](attachments/Pasted%20image%2020220103154339.png)

```java
----------短路与-------------
int a =10;  
int b = 20;  
System.out.println( a>100 && ++b >10);//false  
System.out.println(a);//10  
System.out.println(b);//20, 左边为false, ++b没有执行

----------单个与-----------------
System.out.println( a>100 & ++b >10);//false  
System.out.println(a);//10  
System.out.println(b);//21, 单个与会执行右半部分


----------短路或--------------
System.out.println(a>=10 || ++b<100);//true  
System.out.println(b);//20, 左边为true，++b没有执行 

----------单个或-----------------

System.out.println(a>=10 | ++b<100);//true  
System.out.println(b);//21, 单个或执行右半部分
```



## 7. 三元运算符

```ad-def
条件表达式 ？值1: 值2；

计算条件表达式的结果，true 返回值1； false返回值2
```

```java
int score = 98;  
String rs = score>=60? "pass":"false";  
String rs2 = 58>=60? "pass":"false";  
System.out.println(rs);//pass  
System.out.println(rs2);//false
```
>案例
```java
 返回两者中的较大值
 int a =100;  
 int b = 10;  
 int rs = a>b? a:b;  
 System.out.println(rs);//100  
 }


--------------------------------------------
三个数求最大值  
int a = 10;  
int b = 20;  
int c = 30;  
int temp = a>b? a : b;  
int rs = temp>c? temp :c;  
System.out.println(rs);//30

--------------------------
三元运算符嵌套
int max = a>b? (a>c? a : c):(b>c ? b :c);  
System.out.println(max);//30
```

## 8. 运算优先级

单目乘除位关系，逻辑三目后赋值。

单目运算符:一次作用一个变量的运算符，又叫一元运算符  
单目：单目运算符+ –(正负数) ，++ --，！（逻辑非），~（按位取反）  
乘除：算数运算符：* / % + - （* / %优先级肯定是大于+-的）  
为：位运算符：~（按位取反）<<(左移) >>(右移)，^（也可以位运算，二进制异或）  
关系：关系运算符：> < >= <= == !=  
逻辑：逻辑运算符（除！）&& || & | ^  
三目：条件运算符A > B ? X : Y  
后：无意义，仅仅为了凑字数  
赋值：=  +=  -= *=  /=  %=  |=  &=  ^= 

说明：前优先级大于后，比如单目运算符~也是位运算符，~的优先级是单目级别的。

![](attachments/1.png)

```java
System.out.println(10>3||10>3 && 10<3);//true 先算双与，后双或  
System.out.println((10>3||10>3)&& 10<3);//false 小括号双或，后双与
```

<br/>
<br/>

# API (application programming interface)应用程序编程接口
存在JRE里面
1. java 写好的程序（功能代码）可以直接调用
2. Oracle提供了API文档（说明书）

使用步骤
1. 导入包 import java.util.Scanner
2. 得到扫描对象
Scanner sc = new Scanner(System.in);
3. 创建变量，等待接收用户输入数据
int age = sc.nextInt();
String name = sc.next();


![](attachments/Pasted%20image%2020220103200436.png)

<br/>
<br/>

# 条件语句 if，  switch

## if 条件
条件满足，执行语句体里的代码，不满足，直接跳过if 结构，执行下一行代码

```ad-def
```java
if(条件布尔表达式){ 
//如果布尔表达式为true将执行的语句 
}

if(布尔表达式){ 
//如果布尔表达式的值为true
}else{ 
//如果布尔表达式的值为false
}

if(布尔表达式 1){ 
//如果布尔表达式 1的值为true执行代码 
}else if(布尔表达式 2){
//如果布尔表达式 2的值为true执行代码 
}else if(布尔表达式 3){ 
//如果布尔表达式 3的值为true执行代码 
}else { 
//如果以上布尔表达式都不为true执行代码 
}
```




<br/>
<br/>

## switch 分支
switch case 语句判断一个变量与一系列值中某个值是否相等，每个值称为一个分支。
```ad-def
```java
switch(expression){  
	case value :  
            //代码语句  
		 break;  
	case value :  
            //代码语句  
		 break;   
	 //你可以有任意数量的case语句  
	default : //可选  
		 //代码语句  
 }
```

执行流程

1. 计算表达式的结果值，拿着这个值去与case后的值进行匹配。
2. 匹配哪个case的值为true就执行哪个case,遇到 break就跳出 整个switch分支。
3. 如果case后的值都不匹配则执行 default代码。


>if 更适合做区间匹配
>switch适合做值匹配的分支选择

```ad-n
1.
switch 语句中的变量类型可以是： byte、short、int 或者 char。从 Java SE 7 开始，switch 支持字符串 String 类型了， 不支持double,float, long（因为java小数运算本身不精确，和case没法精准比对）

2. case 给出的值不允许重复，并且必须为字符串常量或字面量。case值的数据类型必须与switch变量的数据类型相同

3. 不要忘记写break，否则会出现穿透现象。

4. default 在没有 case 语句的值和变量值相等的时候执行。default 分支不需要 break 语句。
```

==如果 case 语句块中没有 break 语句时，匹配成功后，从当前 case 开始，后续所有 case 的值都会输出。如果后续的 case 语句块有 break 语句则会跳出判断。==

```java
int i = 1;  
 switch (i){  
            case 1 :  
                System.out.println('1');  
//                break;  
 case 2:  
                System.out.println('2');  
//                break;  
 case 3:  
                System.out.println('3');  
//                break;  
 default:  
                System.out.println("default");
```
```java
输出结果
1
2
3
default

```

>switch 穿透性可以用于某些特殊情况，精简代码

如果代码执行到没有写 break的case块，==执行完后将直接进入下ー个case块执行代码（而且不会进行任何匹配）==，直到遇到 breakオ跳出分支，这就是 switchi的穿透性。

switch穿透性能解决什么问题？
==存在多个case分支的功能代码是一样时==，可以用穿透性把流程集中到同一处处理，这样可以简化代码。

```java
int month = 7;  
switch (month){  
    case 1 :  
    case 3 :  
    case 5 :  
    case 7:  
    case 8 :  
    case 10 :  
    case 12 :  
        System.out.println(month +"月是31天");  
 break; case 2:  
        System.out.println(month + "月有28天");  
 break; case 4:  
    case 6:  
    case 9:  
    case 11:  
        System.out.println(month + "月有30天");  
 break;
```

```java
输出结果
7月是31天
```


<br/>
<br/>

# 循环控制语句
## for 循环
```ad-def
```java
for (初始化语句; 布尔循环条件表达式; 迭代语句){
循环体代码（重复执行的语句）
}

```

![](attachments/Pasted%20image%2020220112095712.png)

```java
// 重复输出3次hello world  
for(int i =0; i<3; i++){  
    System.out.println("Hello world");
/*  
输出结果  
Hello world  
Hello world  
Hello world  
 */
```

>案例 1. 求和1---5
```java
//求和1-5，并输出  
int rs = 0;  
for(int i =1; i< 6; i++){  
    rs += i; //rs = rs + i;  
}  
System.out.println("1---5的和是"+ rs);
//输出结果
//1---5的和是15
```

>案例2. 

```java
//求1-10 奇数和  
int sum = 0;  
for (int i = 1; i <= 10 ; i++) {  
    if (i % 2 != 0) {  
        sum += i;  
 }  
}  
System.out.println("1-10 的奇数和是" + sum);

//输出结果
//1-10 的奇数和是25
```
注意这里==不要把筛选奇数的条件放进for循环布尔条件里==，那样的话，一旦不满足条件就会结束循环，而不是进行下一次循环

```ad-donot
~~for (int i = 1; i <= 10 && i % 2 != 0; i++)~~
```

可以通过改迭代器的值来实现筛选
```java
for (int i = 1; i <= 10; i+=2)
```


> 案例3 水仙花数
> 需求：在控制台输出所有的“水仙花数”，水仙花数必须满足如下2个要求
> 1. 水仙花数是一个三位数
2. 水仙花数的个位、十位、百位的数字立方和等于原数

```java
//3. 水仙花数  
 for (int i = 100; i <= 999 ; i++) {  
        int ge = i % 10;  // 个位数=总数 % 10 
 int shi = i /10 %10;  // 十位数=总数/10 %10
 int bai = i /100;  //百位数=总数/100
 if (ge*ge*ge + shi*shi*shi + bai*bai*bai ==i){  
           System.out.print(i + "\t");
 }

//输出结果
//153  370	371	407	
```
```ad-n
在同一行水平输出数据的时候，记得要加空格，一般用\t表示加一个tab键的空格， ==但是不要用单引号加空格 ' '， 因为字符空格会被当成ASCII码 “空格(Space)的ASCII码值是:32”==， 可以用双引号加空格，这时是字符串，不会参与运算
```


```ad-n
拓展，要求知道水仙花数的个数
定义count变量，统计输出次数，满足条件时count++
```
```java
//3. 水仙花数  
 int count = 0;  
 for (int i = 100; i <= 999 ; i++) {  
        int ge = i % 10;  
 int shi = i /10 %10;  
 int bai = i /100;  
 if (ge*ge*ge + shi*shi*shi + bai*bai*bai ==i){  
            System.out.print(i + "\t");  
 count++;  
 }  
    }  
    System.out.println("\n" +"水仙花数的个数是"+count);  
}
```

<br/>
<br/>


## while 循环

```ad-def
```java
初始化语句;
while( 布尔表达式 ) { 
//循环内容 
迭代语句;
}
```

重复输出3次hello world
```java
int i = 0;  
while (i<3){  
    System.out.println("Hello world");  
 i++;  
}
```

```ad-n
1. while循环因为初始化语句在循环体外，所以多个循环体需要多个初始化变量i，j, k....
2. while循环绝对不要忘记迭代语句，否则会陷入死循环
```
>一般来说，知道需要循环多少次的时候用for循环，
>不知道需要循环多少次的时候用while循环


>案例1. 珠穆朗玛峰
世界最高山峰是珠穆朗玛峰(8848.86米=8848860毫米)，假如我有一张足够大的纸，它的厚度是0.1毫米。请问，折叠多少次，可以折成珠穆朗玛峰的高度

```java
// 案例1：珠穆朗玛峰  
 double i = 0.1;  //纸张高度
 int count = 0;  
 while (i<=8848860){  //当纸张高度小于珠峰高度时
            i = 2*i;// i*= 2  //折叠一次厚度加倍
 count++;  
 }  
        System.out.println("一共需要"+count+"次");  
 System.out.println("纸张的最终厚度是" + i);


//输出结果
//一共需要27次
//纸张的最终厚度是1.34217728E7

```


<br/>
<br/>

## do while 循环
先执行再判断循环条件
```ad-def
```java
初始化语句;
do { 
循环内容 
迭代语句;
}while (循环条件)
```
```ad-n
==do while 循环一定会先执行一次循环！！！==
```
![](attachments/Pasted%20image%2020220114205500.png)


输出3次hello world
```java
int i = 0;  
do {  
    System.out.println("Hello world");  
 i++;  
}while(i<3);
```


##  3种循环的区别对比
![](attachments/Pasted%20image%2020220114210042.png)

## 死循环
一直循环执行下去，没有干预不会停止

常用于服务器（因为它需要一直开着，相当于一个死循环）

定义死循环
```java
经典写法：

while(true){  
    System.out.println("死循环");  
}



方法二：
for( ; ;){  
    System.out.println("死循环2");  
}


方法三：
do{
System.out.println("死循环3");
}while(true);

```

>案例1
>需求：系统密码是666666,请用户输入密码验证，验证不对输出密码错误，并不断继续验证， 验证成功输出欢迎进入系统，并停止程序

```java
int correct_pin = 666666;  
Scanner sc = new Scanner(System.in);//sc 对象是相同的，可以放在外面只创建一次  注意System大写
while(true){  
    System.out.println("请输入密码：");  
 int pin = sc.nextInt();//pin是每次循环都需要输入的，是不同的，放在循环内部  
 if (pin == correct_pin){  
        System.out.println("密码正确，登陆成功");  
 break;//立即结束循环  
 }else{  
        System.out.println("密码错误，请重新输入");  
 }  
}
```

```java
输出结果
请输入密码：
111111
密码错误，请重新输入
请输入密码：
666666
密码正确，登陆成功

```
<br/>
<br/>

## 循环嵌套

> 特点：外部循环每执行一次， 内部循环全部执行完一次

>案例每天3次我爱你，一共五天  

```java
//外部循环是每一天，执行一次， 内部循环执行3次我爱你  
for (int i = 0; i < 5; i++) {  
    System.out.println("第"+ (i+1) + "天");  
 for (int j = 0; j < 3; j++) {  
        System.out.println("我爱你"+ (j+1));  
 }
```

>案例2 打印4行5列*号 

```java
// 案例2 4行5列*号  
for (int i = 0; i < 4; i++) {  
    for (int j = 0; j < 5; j++) {  
        System.out.print("*");  
 }  
    System.out.println();//换行  
}
```



<br/>
<br/>

## break and continue

```ad-def
break: 跳出并结束==当前==所在循环
continue:用于跳出当前循环的当次执行，进入下一次循环。
```

注意：break:只能用于结束当前所在循环，或者结束所在 switch分支的执行；
continue:只能在循环中进行使用。


```ad-n
continue使用的时候，要注意if条件放在循环体前面，先判断是否满足条件，否则先执行了循环再结束当前循环就没意义了
```

> 案例1 洗碗5天，第三天过生日不洗，后面接着洗 
```java
// 洗碗5天，第三天过生日不洗，后面接着洗  
 for (int i = 1; i <=5 ; i++) {  
            if(i==3){  
                System.out.println("过生日，不洗");
continue; }  
            System.out.println("洗碗第"+i + "天");  
 }
```

```java
输出结果
洗碗第1天
洗碗第2天
过生日，不洗
洗碗第4天
洗碗第5天
```

<br/>
<br/>


注意！！在循环嵌套时，如果希望用break,continue结束外部循环，需要在外部循环前面定义标签，然后用break “标签”来结束外部循环


```ad-n
break默认是结束当前循环，有时我们在使用循环时，想通过内层循环里的语句直接跳出外层循环，java提供了使用break直接跳出外层循环，此时需要在break后通过标签指定外层循环。java中的标签是一个紧跟着英文冒号的标识符，与其他语言不同的是，java中的标签只有放在循环语句之前才有作用。需要注意的是，break后标签必须是一个有效的标签，即这个标签须在break语句所在循环的外层循环之前定义。

continue是结束当前循环的单次循环，同理，continue也可以结束外部循环的当前单次循环。

```


# Random 类 随机数字

作用： 用于生成一个随机数字

使用步骤
1. 导包： import java.util.Random;
2. 创建一个新的随机数对象：Random r = new Random();

![](attachments/Pasted%20image%2020220115144329.png)
3. 调用随机数对象，用变量接收值 int i = r.nextInt(10);

nextInt(n) 用于生成0--n-1的随机数


```java
Random r = new Random();  
int i = r.nextInt(10);
```
选中代码
把代码放进循环的快捷键 Ctrl+Alt +t


生成任意区间的随机数的方法
减到0 之后右边界加一找到N, 后面再把减的加回去，

>例如生成3-17 之间的随机数
3-----17
0-----14---n=15
int data = r.nextInt(15)+3;

>拓展：int data = r.nextInt(10, 30); 可以生成10-29的随机数字

>案例
>随机生成一个1-100之间的数字，提示用户猜测，猜大提示过大，猜小提示过小，直到猜中结束游戏。

```java
Random r = new Random();  
//1-100---0-99  
int num = r.nextInt(100)+1;  
System.out.println("答案是"+ num);  
  
Scanner sc = new Scanner(System.in);  
while(true){  
    System.out.println("请输入猜的数字1-100：");  
 int guess = sc.nextInt();  
  
  
 if (guess < num){  
        System.out.println("猜小了");  
 }else if(guess > num) {  
        System.out.println("猜大了");  
 }else if(guess == num){  
        System.out.println("猜对了");  
		break; 
 }
```


<br/>
<br/>

# 数组

## 定义
数组是用来存储固定大小的同一数据类型元素的内存区域。

数组分为  
1. 静态初始化数组： 定义数组的时候就已经赋值。
2. 动态初始化数组：定义数组的时候，只==确定数组的类型和元素个数==，之后再存入数据。


```ad-def
title:静态初始化数组

完整格式：
数据类型 []  数组名 = new 数据类型 [] {元素1， 2，...};

<br/>

简化格式
数据类型 [] 数组名 = {元素1， 2，...};
```
```java
int [] age = new int [] {18, 19, 20};
String [] names = {"tom"}
```



```ad-n
数据类型 [] 数组名”也可以写成 “数据类型 数组名 []”。
```


数组名称变量中存储的是， 数组对象在内存的首地址，数组是==引用类型==。

![](attachments/Pasted%20image%2020220116171645.png)


```java
验证
String [] names = {"tom"};  
System.out.println(names);

输出结果
[Ljava.lang.String;@776ec8df
```

## 数组访问

1. 访问数组值
```ad-def
数组名[索引]
索引从0开始
```

2. 数组长度（元素个数）
```ad-def
数组名.length
```
数组的最大索引可以用 数组名.length-1 来表示（元素个数大于0）

3. 改变数组元素的值
```ad-def
数组名[索引] = 新的赋值
```

```ad-n
注意：数组一旦定义出来，程序执行过程中，数组的==长度，类型==就是固定的！！！
```

## 动态初始化数组
1. 动态初始化数组：定义数组的时候，只==确定数组的类型和元素个数==，之后再存入数据。

```ad-def
title: 动态初始化数组

数据类型 [] 数组名 = new 数据类型[长度];

（其实默认值是0）
```

```java
int [] ages =new int [3];
```

>两种数组定义时的特点和场景有什么区别
当前已经知道存入的元素值，用静态初始化。
当前还不清楚要存入哪些数据，用动态初始化


## 动态初始化数组--元素默认值

<!--
表头|表头|表头
---|:--:|---:
内容|内容|内容
内容|内容|内容
-->

数据类型| 明细| 默认值
:---:|:---:|:---:
基本类型|byte, short, char, int, long|0
基本类型|double, float |0.0
基本类型|boolean|false
引用类型|类，接口，数组，==String==| null

![](attachments/Pasted%20image%2020220116182152.png)

>两种初始化的的使用场景总结、注意事项说明:
>
动态初始化：只指定数组长度，后期赋值，适合开始知道数据的数量，但是不确定具体元素值的业务场景。
>
>静态初始化：开始就存入元素值，适合一开始就能确定元素值的业务场景。
两种格式的写法是独立的，不可以混用。
![](attachments/Pasted%20image%2020220118194103.png)


<br/>
<br/>

## 数组遍历traverse

```ad-def
```java
int [] ages = {20, 30, 40};
for (int i = 0; i < ages.length; i++) {  
    System.out.println(ages[i]);  
}
```

==快捷键 ages.fori  加上tab==



> 案例一：需求：某部门5名员工的销售额分别是：16、26、36、6、100,请计算出他们部门的总销售额

```java
int [] arr = new int[] {16, 26, 36, 6, 100};  
int sum = 0;  
for (int i = 0; i < arr.length; i++) {  
    sum += arr[i];  
}  
System.out.println(sum);

//184
```



<br/>
<br/>

 ## 数组案例

 1. 数组求最值

 求最值的时候，需要定义ー个变量用于记录最值，这个变量建议==默认存储第一个元素值==作为参照。

 不建议自行定义为0， 因为假如都是负数，0会变成最大值，不准确。数据来源于数组本身最好。




 ```java
int [] scores = new int[]{15,9000, 10000, 20000, 9500, -5 };  
int max = scores[0];  
for (int i = 1; i < scores.length; i++) {  //循环从1开始，因为max默认为0号元素
    if (scores[i]> max){  
        max = scores[i];  
 }  
}  
System.out.println("最大值是："+ max); 
```


<br/>
<br/>

2. 案例2：猜数字游戏

需求
开发一个幸运小游戏，游戏规则如下
游戏后台随机生成1-20之间的5个数（无所谓是否重复），然后让大家来猜数字
未猜中提示：“"未命中”，井继续猜测
猜中提示：“运气不错，猜中了”，井输出该数据第一次出现的位置，且输出全部5个数据，最终结束本游戏。

分析
①随机生成5个1-20之间的数据存储起来-->使用数组
②定义ー个死循环，输入数据猜测，遍历数组，判断数据是在数组中，如果在，进行对应提示并结束死循环；如果没有猜中，提示继续猜测直到猜中为止。


```ad-n
break默认是结束当前循环，有时我们在使用循环时，想通过内层循环里的语句直接跳出外层循环，java提供了使用==break label==直接跳出外层循环，此时需要在break后通过标签指定外层循环。java中的标签是一个紧跟着英文冒号的标识符==label :==，与其他语言不同的是，java中的标签只有放在循环语句之前才有作用。需要注意的是，break后标签必须是一个有效的标签，==即这个标签须在break语句所在循环的外层循环之前定义==。

continue是结束当前循环的单次循环，同理，continue也可以结束外部循环的当前单次循环。

```


注意！！在循环嵌套时，如果希望用break,continue结束外部循环，需要在外部循环前面定义标签，然后用break label 来结束外部循环

```java

//1. 随机生成5个1-20之间的数据存储起来-->使用数组
Random r = new Random();  
 int [] nums = new int [5];  
 //动态初始化 得到5个随机幸运数字  
 for (int i = 0; i < nums.length; i++) {  
            nums[i] = r.nextInt(20)+1;  
 System.out.print(nums[i]+"\t");  //给自己看的，不需要其实
 }  
        System.out.println();  
  
  
 Scanner sc = new Scanner(System.in);  
  
// 2. 用死循环来实现一直猜，而不是用for循环，不然会用每次输入和对应i的值比较  
 OUT:// break label 用来结束外部循环  
 while(true) {  
            System.out.println("请猜出幸运数字1-20：");  
 int input = sc.nextInt();  
  
 //外部输入一次，和所有i值比较一次，遍历数组  
 for (int i = 0; i < nums.length; i++) {  
                if (input == nums[i]){  
                    System.out.println("猜对了！幸运数字索引是"+ i );  
//                    System.out.println("所有幸运数字为：");  
//                    for (int j = 0; j < nums.length; j++) {  
//                        System.out.print(nums[j] + "\t");  
//                    }放在循环外面，代码更简洁干净  
 break OUT;}  
            }  
  
            System.out.println("猜错了继续猜");  
 }  
        //循环结束，代表猜对了，可以公布答案  
 System.out.println("所有幸运数字为：");  
 for (int j = 0; j < nums.length; j++) {  
                        System.out.print(nums[j] + "\t");  
 }
```


<br/>
<br/>

3. 案例3：随机排名

![](attachments/Pasted%20image%2020220119173605.png)

分析
①在程序中录入5名员工的工号存储起来-->使用数组。
②依次遍历数组中的每个元素，每次都随机一个索引数据，让当前元素与该索引位置处的元素进行交换。


==注意，1. 打乱顺序是通过元素随机交换实现的
2.元素交换值注意中间变量的使用==


```java
int [] ids = new int[5];  
Random r = new Random();  
Scanner sc = new Scanner(System.in);  
  
//录入数据  
  
for (int i = 0; i < ids.length; i++) {  
    System.out.println("请录入第"+ (i+1) + "名学生学号");  
 ids[i] = sc.nextInt();  
}  
  
//看看数组结果  
System.out.println("参与的学生学号是");  
for (int i = 0; i < ids.length; i++) {  
    System.out.print(ids[i] + "\t");  
}  
System.out.println();  
  
// 打乱顺序--交换两个位置上的值  
for (int i = 0; i < ids.length; i++) {  
    int j = r.nextInt(ids.length);//用length比5更好  
 //定义一个中间变量，存索引j处的数据  
 int mid = ids [j];  
 ids [j] = ids[i];  
 ids [i] = mid;  
}  
  
//看看数组结果  
System.out.println("打乱排序后是：");  
for (int i = 0; i < ids.length; i++) {  
    System.out.print(ids[i] + "\t");  
}  
System.out.println();
```

随机排名还可以用于比如：扑克牌洗牌


<br/>
<br/>

## 数组排序
数组排序就是对数组中的元素，进行升序（从小到大），或者降序（从大到小）的操作。

数组的排序技术
- 冒泡排序
- 选择排序
- 快速排序
- 插入排序
- ...


数组的搜索技术
- 二分查找
- 分块查找
- 哈希表查找
- ...


### 冒泡排序法
原理：比较两个相邻的元素，将值大的元素交换到右边

==特点：N个数字要排序完成，总共进行N-1趟排序，第 i 趟的排序次数为(N-i)次。(i 从1开始) N=array.length==


所以可以用双重循环语句，外层控制循环多少趟，内层控制每一趟的循环次数 

i=1 开始时
外部循环 for (i=1; i<arr.length; i++)
内部循环			for (j =0; j < arr.length-i; j++ )

i=0 开始时
外部循环 for (i=0; i<arr.length-1; i++)
内部循环			for (j =0; j < arr.length-1 -i; j++ )


(2)冒泡排序的优点：每进行一趟排序，就会少比较一次，因为每进行一趟排序都会找出一个较大值。如上例：第一趟比较之后，排在最后的一个数一定是最大的一个数，第二趟排序的时候，只需要比较除了最后一个数以外的其他的数，同样也能找出一个最大的数排在参与第二趟比较的数后面，第三趟比较的时候，只需要比较除了最后两个数以外的其他的数，以此类推……也就是说，没进行一趟比较，每一趟少比较一次，一定程度上减少了算法的量。



![](attachments/Pasted%20image%2020220122094759.png)


```java
 int [] arr = {5, 2, 3, 1};  
 //             0, 1,2, 3  
  
 //外部循环，确定是第几次排序, 4个数字，排3次  
 for (int i = 0; (i < arr.length-1); i++) {  
            //内部循环，每次排序，都从第一个值开始， 让这个值和每一个做比较  
 /*  
 i = 0 j= 0, 1, 2    3 
 i = 1, j =0, 1,     2 
 i = 2 ,j = 0        1 */
//            for (int j = 0; j < (arr.length-1); j++) { // 不要用length-1，这样会有多余的比较，例如i=2时后面的不需要排序  
 for (int j = 0; j < (arr.length-1-i); j++) {//每轮循环次数 n-i（i从1开始）  
 if (arr[j]>arr[j+1]){  
                    int temp = arr[j+1];  
 arr[j+1] = arr[j];  
 arr[j] = temp;  
 }  
            }  
        }  
        //输出数组看看  
 for (int i = 0; i < arr.length; i++) {  
            System.out.println(arr[i]);  
 }

```


<br/>
<br/>

## 数组内存

### java 内存

- 栈
- 堆
- 方法区
- 本地方法栈
- 寄存器


栈：存正在运行的方法， 局部变量，引用数据类型

一般来说，基本数据类型直接在栈中分配空间，局部变量（在方法代码段中定义的变量）也在栈中直接分配空间，当局部变量所在方法执行完成之后该空间便立刻被JVM回收，还有一种是==引用数据类型，即我们通常所说的需要用关键字new创建出来的对象所对应的引用也是在栈空间中（例如数组名）==，此时，JVM在栈空间中给对象引用分配了一个地址空间（相当于一个门牌号，通过这个门牌号就可以找到你家），在堆空间中给该引用的对象分配一个空间，栈空间中的地址引用指向了堆空间中的对象区（通过门牌号找住址）；

堆：一般用来存放用关键字new出来的数据。

方法区：class文件 、存放类的信息（代码）、类的成员变量与成员方法也被加载到方法区中, static变量、常量池（字符串常量）等

![](attachments/Pasted%20image%2020220122102340.png)


### 数组内存
以数组为例，观察java内存分配

![](attachments/Pasted%20image%2020220122102728.png)



### 两个数组变量指向同一个数组对象
因为数组变量名存储的是数组对象的地址
如果把数组变量arr1赋值给arr2
赋值的是地址
而不是产生一个新数组！！！


而两个地址相同，会指向同一个数组对象
所以对任意一个数组变量的任何操作，最终都作用在同一个数组身上

![](attachments/Pasted%20image%2020220122103309.png)


![](attachments/Pasted%20image%2020220122104027.png)
```java
int [] arr1 = new int[]{11, 22, 33};  
System.out.println("arr1"+ arr1);  
  
int [] arr2 = arr1;  
System.out.println("arr2"+ arr2);  
  
arr2[1] = 100;  
  
System.out.println("arr1[1]" + arr1[1]);



输出结果
arr1[I@6d311334
arr2[I@6d311334
arr1[1]100

```

<br/>
<br/>

## 数组使用常见问题

1. 问题1:如果访问的元素位置超过最大索引，执行时会出现 Arraylndexoutof Boundsexception（数组索引越界异常）

![](attachments/Pasted%20image%2020220122104451.png)


2. 问题2:如果数组变量中没有存储数组的地址，而是null, 在访问数组信息时会出现 Nullpointerexception（空指针异常）


![](attachments/Pasted%20image%2020220122104950.png)

相当于把连接栈和堆的线删掉了
![](attachments/Pasted%20image%2020220122105136.png)

但是一个指针坏了不影响另一个
```java
arr2 = null;  
System.out.println(arr1[0]);//11  
System.out.println(arr2[0]);//Cannot load from int array because "arr2" is null
```




<br/>
<br/>
<br/>
<br/>

# 方法
方法是一种语法结构，它可以把一段代码封装成一个功能，方便重复调用。

方法的优点：

1. 使程序变得更简短而清晰。
2. 有利于程序维护。
3. 可以提高程序开发的效率。
4. 提高了代码的==重用性==。


<br/>
<br/>



## 方法的定义和调用

### 定义
```ad-def
title: 方法

修饰符 　返回值类型　方法名 (参数类型 参数名){

	方法体（代码）
	return 返回值
}
```
例如：

![](attachments/Pasted%20image%2020220122151302.png)

注意：
- 方法的名字的第一个单词应以小写字母作为开头，后面的单词则用大写字母开头写，不使用连接符。
-   方法申明了返回值的类型，内部必须使用return 返回相应类型的数据。
- 形参列表可以有多个，甚至可以没有；如果有多个形参，多个形参必须用“，"隔开，且不能给初始化值。


<br/>
<br/>


-   方法包含于类或对象中
-   方法在程序中被创建，在其他地方被引用


***==方法直接定义在类里！！不要定义在main 方法里==***


方法的其他写法：

方法定义时：返回值类型、形参列表可以按照需求进行填写。

1. 可以无返回值，定义的时候返回值类型写做void, 此时方法内部不可以使用 return返回数据。
2. 可以无参数，直接空着
3. 方法如果没有参数，或者返回值类型申明为void可以称为无参数、无返回值的方法，依次类推。

```java

public class method {  
    public static void main(String[] args) {  
        // main 方法里调用  
 helloworld();  
 }

// 无参数，无返回值方法  
public static void helloworld (){  
    System.out.println("hello world");  
 System.out.println("hello world");  
 System.out.println("hello world");
}  
}
```









<br/>
<br/>



### 调用
>方法名（参数数据）

当程序调用一个方法时，程序的控制权交给了被调用的方法。当被调用方法的返回语句执行或者到达方法体闭括号时候交还控制权给程序。


当方法返回一个值的时候，方法调用通常被当做一个值。例如：

int larger = max(30, 40);

如果方法返回值是void，方法调用一定是一条语句。例如，方法println返回void。下面的调用是个语句：

System.out.println("欢迎访问菜鸟教程！");

```java
public class method {  
    public static void main(String[] args) {  
        // main 方法里调用  
 int result = sum(100,200);  
 System.out.println( result);  
 }  
  
        //main外面 定义求和方法  
 public static int sum(int a, int b){  
            int c = a +b;  
 return c;  
 }  
}
```


<br/>
<br/>
<br/>
<br/>



## 方法使用常见问题

方法常见问题

1. 方法编写时顺序无所谓。（只要方法定义了即可，不需要定义写在调用上面）

```java
public class method {  
    public static void main(String[] args) {  
        // main 方法里调用  
 int result = sum(100,200);  
 System.out.println( result);  
 }  
  
        //main外面 定义求和方法  
 public static int sum(int a, int b){  
            int c = a +b;  
 return c;  
 }  
}
```
<br/>
<br/>



2. 方法与方法之间是平级关系，不能嵌套定义。
==方法A不能定义在方法B 里面==。比如不能定义在main方法里面。

<br/>





3. 方法的返回值类型为void（无返回值），方法内则不能使用 return返回数据，（有return会报错）
如果方法的返回值类型写了具体类型，方法内部则==**必须使用 return 返回对应类型的数据。**==（没有rerun也会报错Missing return statement）

<br/>






4. return语句下面，不能编写代码，因为永远执行不到，属于无效的代码。
5. Java中return用于方法，两个作用：
 （1）返回方法指定类型的值（这个值总是确定的），也可以是对象  
   （2）结束方法的执行（仅仅一个return语句）

<br/>



6. 方法不调用就不执行，调用时必须严格匹配方法的参数情况。

<br/>



7. 有返回值的方法调用时可以选择定义变量接收结果，或者直接输出调用，甚至直接调用；无返回值方法的调用只能直接调用一下。

```java
int result = sum(100,200);//用变量接收  
System.out.println( sum(10, 20));//直接输出调用  
sum(50,60);//直接调用，只是调用方法，让方法跑一下，但是方法返回的结果没要 


helloworld();//无返回值方法的调用只能直接调用一下。是statement
```

<br/>
<br/>

## 方法案例

> 案例1：定义一个方法，计算1，2,....n 的和并返回

分析
1.根据格式编写方法---->关注参数和返回
因n不固定，故方法需要声明形参接收；要返回结果，还需申明返回值类型
2.方法内部使用for循环计算出1-n的和并返回。

```java
public static int add (int n){  
    int sum = 0;  
 for (int i = 1; i <= n; i++) {  
        sum += i;  
 }  
    return sum;  
}




public static void main(String[] args) {  
    //-------------------------------------------案例1：1---n求和  
 int sum = add(100);  
 System.out.println(sum);//5050
}
```

<br/>
<br/>

>案例2：需求：拿一个整数，然后调用方法，把整数交给方法在方法中输出该数为奇数还是偶数。

分析
1.根据格式编写方法，因要传入数据给方法，方法需要声明形参接收。直接在方法中输出结果即可，不需要返回值
2.方法内部使用if语句判断，并输出对应的结论。


```java
public static void evenOrodd (int a){  
        if (a%2 == 0){  
            System.out.println("数字" + a + "是偶数");  
 }else{  
            System.out.println("数字" + a + "是奇数");  
 }  
}



public static void main(String[] args) {
//案例2 ： 判断奇偶性并返回  
evenOrodd(1);//数字1是奇数  
evenOrodd(0);//数字0是偶数
}
```

<br/>
<br/>

>案例3： 需求
把找出数组的最大值案例，改造成方法，可以支持返回==任意整型数组==的最大值数据。

分析
1.根据格式编写方法
要返回最大值，需要申明返回值类型。
需要接收数组，需要申明形参列表
2.方法内部找出数组的最大值并返回。


```java
/定义
public static int getArrayMax(int [] arr){  
    int max = arr[0];  
 for (int i = 1; i < arr.length; i++) {  
        if (max < arr[i]){  
            max = arr[i];  
 }  
    }  
    return max;  
}


// 调用
int [] ages = {10, 30, 40, 100};  
int max = getArrayMax(ages);  
System.out.println(max);//100
```

流程：定义数组ages, 调用函数getArrayMax， ages传递给参数arr， **==传递的是地址， 此时是两个数组变量指向同一个数组内存==**


<br/>
<br/>

<br/>
<br/>

## 方法内存原理
方法的调用流程-内存图解
- 方法没有被调用的时候，在==***方法区***==中的字节码文件中存放
- 方法被调用的时候，需要进入到==***栈内存***==中运行


可以理解为，方法没有被调用时就像子弹存在弹夹里
调用时，子弹上膛，进入枪膛里。
![](attachments/Pasted%20image%2020220123103832.png)



> 以求和函数为例

1. 没有运行时，方法区存放了class文件，还有main方法，add方法。
2. 运行时，首先运行main方法，进入栈内存中，
3. 然后调用add方法，进入栈中
4. 运行完成后方法会从栈中退出。（用完一个立马退一个）

![](attachments/Pasted%20image%2020220123104129.png)
详情可见
https://www.bilibili.com/video/BV1Cv411372m?p=58


<br/>
<br/>

<br/>
<br/>

## 方法参数传递机制
java 参数传递机制分两种 
- 基本类型的参数传递
- 引用类型的参数传递

### 1. **基本类型和引用类型在内存中的保存**
Java中数据类型分为两大类，**基本类型和引用类型**。相应的，变量也有两种类型：基本类型和引用类型。  

基本类型的变量保存原始值，即它代表的值就是数值本身；原始值一般对应在内存上的栈区。

基本类型-->原始值--> 栈区

而引用类型的变量保存引用值（在栈区），"引用值"指向内存空间的地址，代表了某个对象的引用，而不是对象本身，  
对象本身存放在这个引用值所表示的地址的位置，在内存上的堆内存区。

引用类型-->引用值：存储对象在堆内存区的地址-->自身存在栈区　　　　　　　
对象本身--> 存数据-->在堆内存
			
**基本类型包括：byte,short,int,long,char,float,double,Boolean,returnAddress，**  
**引用类型包括：类类型，接口类型和数组。**

相应的，变量也有两种类型：基本类型和引用类型。


<br/>
<br/>


### 2. 基本类型的参数传递
```ad-n
Java的参数传递机制：值传递
在传输实参给方法的形参的时候，并不是传输实参变量本身，而是传输实参变量中存储的值，这就是值传递。

```
**形参** ：就是形式参数，用于定义方法的时候使用的参数，是用来接收调用者传递的参数的。在整个函数体内都可以使用，离开该函数则不能使用。

实参：实参出现在**主调函数中，进入被调函数后，实参变量也不能使用**。
实参可以是常量、变量、表达式、函数等，无论实参是何种类型的量，在进行函数调用时，它们都必须有确定的值，以便把这些值传送给形参。因此应预先用赋值，输入等办法使参数获得确定值。



>值传递：方法调用时，实际参数把它的值传递给对应的形式参数，函数接收的是原始值的一个==copy==， 此时内存中存在两个相等的基本类型，即实际参数和形式参数，==后面方法中的操作都是对形参这个值的修改，不影响实际参数的值。==


```java

int a =10;  
System.out.println("调用前a= " + a);//调用前a=10  
change(a);  
System.out.println("调用后a=" + a);//调用后a=10




public static void change(int a){  
 System.out.println("调用函数，传递来的a="+ a);  //调用函数，传递来的a=10
 a = 20;  
 System.out.println("函数内部更改a后，a =" + a);  //函数内部更改a后，a =20
}
```

函数接收的是原始值的一个==copy==， 此时内存中存在两个相等的基本类型，即实际参数和形式参数，后续在调用函数内部，对形参的操作，都不影响下面实参的值

![](attachments/1%201.png)
<br/>
<br/>

### 3. 引用类型的参数传递
```ad-n
title: 引用传递
方法调用时，实际参数中存储的的引用(地址，而不是参数的值)被传递给方法中相对应的形式参数，函数接收的是原始值的内存地址

**在方法执行中，形参和实参内容相同，指向同一块内存地址，方法执行中对引用的操将会影响到实际对象**。

```
本质上也是值传递，但是传递的是地址值。



```java

int [] arr = new int[]{10, 20, 30};  
System.out.println("调用函数前，数组第一个值为"+ arr[0]);//调用函数前，数组第一个值为10  
change2(arr);  
System.out.println("调用方法后，数组第一个值为" + arr[0]);//调用方法后，数组第一个值为11111



public static void change2(int [] arr){  
    System.out.println("调用方法，传递来的数组第一个值是" + arr[0]);  //调用方法，传递来的数组第一个值是10
 arr[0] = 11111;  
 System.out.println("方法内部更改数组第一个值后，是"+ + arr[0]);  //方法内部更改数组第一个值后，是11111
}
```

![](attachments/Pasted%20image%2020220123154519.png)

<br/>
<br/>

<br/>
<br/>

## 方法参数传递案例
> 案例1 ：需求
设计一个方法用于输出任意整型数组的内容，要求输出成如下格式
“该数组内容为：[11,22,33,44,55]”

分析
1、定义一个方法，要求该方法能够接收数组，并输出数组内容
需要参数吗？需要返回值类型申明吗？

--需要参数接收数组， 但不需要返回值，可以直接打印

2、定义一个静态初始化的数组，调用该方法，并传入该数组。


```java

int [] arr = new int[]{ 11, 22, 33, 44, 55};  
printarray(arr);

public static void printarray(int [] arr){  
        System.out.print("该数组内容为：[");  
 for (int i = 0; i < arr.length; i++) {  
//            System.out.print(arr[i] +", ");// [11, 22, 33, 44, 55, ]最后会多一个逗号，不要用两个循环来分别打印arr[i]和逗号，加个条件语句即可  
 if(i== arr.length-1){  
                System.out.print(arr[i]);  
 }else{  
                System.out.print(arr[i] +", ");  
 }  
        }  
        System.out.println("]");  
 }
```
注意，上面的条件部分，可以用三元运算符代替！简化代码

```
条件表达式 ？值1: 值2；

计算条件表达式的结果，true 返回值1； false返回值2
```
三元运算符是运算符！！==返回的是值！！！==
不要把打印语句放在后面的值的位置，而是放在前面，先是打印命令，打印的是什么呢？ 是三元运算符返回的值。

额外补充，保证数组非空指针null且长度大于零

```java
public static void printarray(int [] arr){  
        System.out.print("该数组内容为：[");  

if(arr != null && arr.length > 0){  
            for (int i = 0; i < arr.length; i++) {  
//            System.out.print(arr[i] +", ");// [11, 22, 33, 44, 55, ]最后会多一个逗号，不要用两个循环来分别打印arr[i]和逗号，加个条件语句即可  
//            if(i== arr.length-1){  
//                System.out.print(arr[i]);  
//            }else{  
//                System.out.print(arr[i] +", ");  
//            }  
 System.out.print(i == arr.length-1? arr[i] : arr[i] +", ");  
 }  
        }
		System.out.println("]");  
 }
```

<br/>
<br/>

>案例2： 需求
设计一个方法可以查询元素值在数组中的索引；最终要返回元素在该数组中的索引，如果数组中不存在该元素则返回-1

![](attachments/Pasted%20image%2020220123174351.png)

分析
1、定义方法，接收整型数组，查询的元素值，在方法体中完成元素查询的功能。--->是否需要参数、返
回值类型？

-- 需要接收参数，2个，并且也需要返回值 ，2种

2、定义数组，调用该方法，并指定要搜索的元素值，得到返回的结果输出。

问题1： num要和每一个值比较，相同输出i，但不同的时候要所有值都不同才输出-1  
>解决方法， 不同的时候要和所有值都不同，*那就放在循环外面*

问题2： return的使用，它结束方法了，怎么条件返回两个值? 而且必须在for外面return？
>注意一个误区：***return可以不只有一个！*** return可以结束方法，但可以不只有一个， （比如存在不同条件下不同return）， 先执行到的return就会直接跳出代码块，不再执行代码块以下的其他代码

```ad-n
title: 正确答案
```

```java
int [] arr = new int[]{ 11, 22, 33, 44, 55};  
System.out.println(checkIndex(arr, 11));  //0
System.out.println(checkIndex(arr, 10));  //-1


public static int checkIndex(int [] arr, int num){  
        for (int i = 0; i < arr.length; i++) {  
            if (arr[i] == num) {  
                return i;  
 }  
        }  
        return -1;  
}
```
<br/>
<br/>

```ad-donot

并不是必须要在for循环外return, 但是for 循环搭配return会有坑。

以下面**错误代码**为例：
```java
public static int checkIndex(int [] arr, int num){  
        for (int i = 0; i < arr.length; i++) {  
            if (arr[i] == num) {  
                return 0;  
			 }else{  
                return -1;  
			 }  
		    }  
}
//报错Missing return statement
```


1. 首先假设不考虑按照上面代码的写法，for循环只能执行一次的问题，仅仅来讨论一下，为什么报错报的是Missing return statement
2. 看起来这个方法，只要得到数组参数arr，进入方法就进for循环遍历，只要进入循环，无论是满足条件arr[i] == num进入if，或者不满足进入else，都有对应的return,为什么还会提示没有return 呢？

>原因是for循环的条件不一定满足，条件不满足的时候是不会执行循环体语句的！（例如传入一个空数组，length=0）这时会直接跳过循环，而这种情况下，方法并没有return，所以会报错


![](attachments/Pasted%20image%2020220112095712.png)


证明：假如在刚才代码的基础上，for循环外面再加一个return，传入一个空数组，看是否是预计的结果，这样可以证明我们刚才关于for循环使用return的猜测是否正确
```java
public static int checkIndex(int [] arr, int num){  
        for (int i = 0; i < arr.length; i++) {  
            if (arr[i] == num) {  
                return 0;  
 }else{  
                return -1;  
 }  
        }  
        return 2;  
}


// 空数组  
int [] arr2 = {};  
System.out.println(arr2.length);  //0
System.out.println(checkIndex(arr2, 1));//2
```

当然，即使考虑空数组也没必要写成上面这样，最开始的正确答案可以直接return -1.


此外，类似的还有条件语句需要注意，只有if， 没有else的时候，必须要写成情况1的形式，java认为if不会有任何情况下都能执行的能力。

而有else，java编译器对if else 语句能够全面囊括所有情况的能力只限定在的if...else【情况2】(或if...else if...else)【情况3】时，而不包括if...else if。即使你把所有条件都列出来，它也不认为涵盖所有情况

情况1和情况2是完全相同的。

```java

*******情况1
if(){
	return 1;
}
return 2；

*******情况2
if (){
	return 1;
}else {
	return 2；
}

*******情况3
if (){
	return 1;
}else if{
	return 2；
}else{
	return 3;
}
```



<br/>
<br/>

> 案例3：
需求
如果两个数组的类型，元素个数，元素顺序和内容是一样的我们就认为这2个数组是一模一样的。请使用方法完成：能够判断任意两个整型数组是否一样，并返回true或者 false。

![](attachments/Pasted%20image%2020220126224235.png)

分析
1、定义方法-->是否需要参数、返回值类型？

--需要接收参数，2个整型数组，需要布尔类型返回值

2、在方法内部完成判断的逻辑，并返回布尔结果。

问题1：java怎么判定相等，是值相等就是相等，还是包括元素类型？
>解决方法：因为传入参数都是整型数组，保证了元素类型一样。

问题2：因为不知道两个数组的长度，所以随便拿任意一个做循环的坐标都是不合适的，比如
```java
int [] arr1 = new int [] {1, 2, 3};  
int [] arr2 = new int [] {1, 2, 3, 4};
```
如果用arr1做循环的坐标
```java
public static boolean equalityCheck (int [] arr1, int [] arr2){  
    for (int i = 0; i< arr1.length; i++){  
        if (arr1[i] != arr2[i]){  
            return false;  
 }  
    }  
    return true;  
}
```
这样结果会有问题，arr1的索引只到2，在它索引范围内值都相同，但是实际上两数组并不一样

> 解决方法：先判断数组长度是否相同，相同的情况下再选任意一个数组遍历。


```ad-n 
title:正确答案
```

```ad-n
注意的问题
1： for循环中，if搭配return的时候，如果满足条件就返回会造成循环只能执行一次，注意要选择条件不满足才返回，直接结束循环。

2：当循环都执行完了，仍没有false，证明结果一定是true.

3. 注意考虑for循环不满足循环条件时的返回值。

```

```java

//自己的答案
public static boolean equalityCheck (int [] arr1, int [] arr2){  
    if (arr1.length != arr2.length){  //注意条件要写不等于
        return false;  
 }  //长度相等才能向下执行
    for (int i = 0; i< arr1.length; i++){  
        if (arr1[i] != arr2[i]){  
            return false;  
 }  
    }  
    return true;  // 
}

//标准答案
public static boolean equalityCheck2 (int[] arr1, int[] arr2){  
    if(arr1.length == arr2.length){//长度相等才比较  
 for (int i = 0; i < arr1.length; i++){  
            if (arr1[i] != arr2[i]) {  
                return false;//元素不等就false  
 }  
        }  
        return true;//所有的都遍历一次没有false，一定是true.  
 }  
    return false;//长度不等，或者不满足循环条件等其他情况，都是false  
}

```


<br/>
<br/>

<br/>
<br/>

## 方法重载
同一个类中，出现多个方法***名称相同，但是形参列表是不同的***，那么这些方法就是重载方法。
调用方法的时候会通过参数的不同来区分调用的具体是哪个方法。

案例导学
开发武器系统，功能需求如下
①可以默认发一枚武器。
②可以指定地区发射一枚武器。
③可以指定地区发射多枚武器。

```java
public static void fire(){  
    System.out.println("默认发射一枚导弹");  
}  
  
public static void fire(String location){// 形参：数据类型 形参名  
 System.out.println("指定地点" + location +"默认发射一枚导弹");  
}  
  
public static void fire(String location, int num){  
    System.out.println("指定地点" + location + "发射"+ num + "枚导弹");  
}


fire();  
String l1 = "沙漠";  
fire(l1);  
fire("不用变量行吗", 3);//行，可以是字符串，也可以是字符串变量，等同于直接传入数字1，和int num =1; 传入num;

结果
默认发射一枚导弹
指定地点沙漠默认发射一枚导弹
指定地点不用变量行吗发射3枚导弹
```

还可以在方法中调用重载方法
例如：
```java
public static void fire(String location){// 形参：数据类型 形参名  
 System.out.println("指定地点" + location +"默认发射一枚导弹");  
}  

可以改写为
public static void fire(String location){// 形参：数据类型 形参名  
fire(location, 1);  
}  

结果：
指定地点沙漠发射1枚导弹
```

方法重载的优点：

对于相似功能的业务场景：可读性好，方法名称相同提示是同一类型的功能，通过形参不同实现功能差异化的选择，这是一种专业的代码设计。


<br/>
<br/>

### 方法重载的识别技巧
1. 只要是同一个类中，方法***名称相同、形参列表不同***，那么他们就是重载的方法，其他都不管！(如：修饰符，返回值类型都无所谓)
2. 形参列表不同指的是：形参的**个数、类型***、***顺序***不同，不关心形参的名称。
```java
1. public static void open () {}//原始方法
2. public static void open(int a){}//是重载，形参个数不同
3. static void open(int a, int b){}//是重载，形参个数不同
4. public static void open(double a, int b){}//是重载，数据类型不同
5. public static void open(int a, double b){}//是重载，形参顺序不同
6. public void open(int i, double d){}//不是重载，形参和5同，重复方法
7. public static void OPEN(){}//不是重载，方法名称不同，区分大小写，新方法
```



<br/>
<br/>



### return 单独使用

>return关键字单独使用，不需要返回值：return; 
>可以立即跳出并结束当前方法的执行；
> return关键字单独使用可以放在任何方法中。

![](attachments/Pasted%20image%2020220209215419.png)
<br/>
<br/>

<br/>
<br/>



# 编程案例

## 案例1：买飞机票
需求
机票价格按照淡季旺季、头等舱和经济舱收费、输入机票原价、月份和头等舱或经济舱。
按照如下规则计算机票价格：旺季(5-10月)头等舱9折，经济舱8.5折，淡季(11月到来年4月)头等舱7折，经济舱6.5折。

自己分析：
1. 定义方法，有参数3个：原价，月份，经济or头等舱， 有返回值：最终票价
2. 用switch case 来分月份，利用穿透性

```ad-n
==比较的是两个字符串的地址是否为相等（同一个地址），equals()方法比较的是两个字符串对象的内容是否相同（当然，若两个字符串引用同一个地址，使用equals()比较也返回true）。

要比较字符串内容是否相等，应该用 string的equals方法

```

```java
public class cases {  
    public static void main(String[] args) {  
        // 手动输入原价,月份和头等舱或经济舱。  
 Scanner sc = new Scanner(System.in);  
  
 System.out.println("请输入机票原价");  
 double originPrice = sc.nextDouble();  
 System.out.println("请输入月份");  
 int month = sc.nextInt();  
 System.out.println("请输入飞机舱型，经济舱或头等舱");  
 String classes = sc.next();  
 System.out.println("您的机票优惠后价格为；" + price(originPrice, month, classes) );  
 }  
  
    public static double price(double originPrice, int month, String classes){  
        double price =0;  
 // 淡季  
 switch (month){  
            case 1:  
            case 2:  
            case 3:  
            case 4:  
            case 11:  
            case 12:  
//                if (classes == "经济舱"){// 不行，==比较内存地址  
 if (classes.equals("经济舱") ){// equals比较内容  
 price = originPrice * 0.65;  
 }else if(classes.equals("头等舱") ){  
                    price = originPrice * 0.7;  
 }else{  
                System.out.println("舱型有误，请重新输入");  
 price = -1;  
 }  
                break;  
 case 5:  
            case 6:  
            case 7:  
            case 8:  
            case 9:  
            case 10:  
                if (classes.equals("经济舱")){  
                    price = originPrice * 0.85;  
 }else if(classes.equals("头等舱") ){  
                price = originPrice * 0.9;  
 }else{  
                System.out.println("舱型有误，请重新输入");  
 price = -1;  
 }  
                break;  
 }  
        return price;  
 }  
  
  
}
```
>缺点：用switch case 分支来确定月份代码太长，繁琐， 中间的price可以用*=
>注意：== 和equals的使用。对引用类型数据，== 比较内存地址， equals比较对象的值。


答案分析
1. 键盘录入机票原价、月份和机舱类型
2. 使用判断月份是是旺季还是淡季，使用 switch分支判断是头等舱还是经济舱。
3. 选择对应的折扣进行计算并返回计算的结果。

```java
public static double cal(double money, int month, String type){  
        if(month >=5 && month <=10){  
            switch(type){  
                case "经济舱":  
                    money *= 0.85;  
 break; case "头等舱":  
                    money *= 0.9;  
 break; default:  
                    System.out.println("输入舱型有误，请重新输入头等舱或经济舱");  
 money = -1;  
 }  
        } else if(month >=1 && month <=4 || month ==11 || month==12){  
            switch (type){  
                case "经济舱":  
                    money *= 0.65;  
 break; case "头等舱":  
                    money *= 0.7;  
 break; default:  
                    System.out.println("输入舱型有误，请重新输入头等舱或经济舱");  
 money = -1;  
 }  
            }else{  
            System.out.println("您输入的月份有误，请重新输入1-12");  
 money = -1;  
 }  
        return money;  
 }  
}
```
>注意，case值比较，从 Java SE 7 开始，switch 支持字符串 String 类型了，同时 case 标签必须为字符串常量或字面量。可以直接比较字符串的内容。

