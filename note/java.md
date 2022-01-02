# 运算符
![](attachments/Pasted%20image%2020220102222845.png)
除法默认结果是整数，因为表达式的最终结果由表达式的最高类型决定，整数默认为int型，除法表达式的结果也是int整数，含有小数的结果自动舍弃小数部分。

```java
int a =10;  
int b =3;  
System.out.println(a+b);//13  
System.out.println(a-b);//7  
System.out.println(a*b);//30  
System.out.println(a/b);//3-----因为3.3333自动转换为

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


