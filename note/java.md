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
 //十位 123/10/10 取余  
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


# if 条件
条件满足，执行语句体里的代码，不满足，直接跳过if 结构，执行下一行代码

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


