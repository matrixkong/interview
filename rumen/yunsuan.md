# 第一章 运算

## 第一节

提示1-7 ： 对于常量尽量设为 final 比如 圆周率pi， 这样就可以对变量性质一目了然

## 第二节

### 例题 1-2：reverse integer 

```java
public int reverse (int input)
	{
		int result  = 0;
		while(input !=0)
		{
			if((result > Integer.MAX_VALUE/10) 
				|| (result == Integer.MAX_VALUE/10 && input%10 >Integer.MAX_VALUE%10)) 
					return -1;
			result = result*10 + input%10; 
			input = intput/10;
		}
		return result;
	} 
```

### 例题 1-3： swap number 这个是个很常用的方法，我一般用 三变量法

```java
public void swap (int[] arr, int i ,int j)
{
    if(arr == null ) return ;
	if(arr.length <= Math.max(i,j)) return ;
	int temp = arr[i];
	arr[i] = arr[j];
	arr[j] = temp;
}
```

书上还介绍了另一个方法，就是在数组元素可以加减的情况下，可以通过两个元素的加减来swap。

```java
public void swap (int[] arr, int i ,int j)
{
	if(arr == null ) return ;
	if(arr.length <= Math.max(i,j)) return ;
	arr[i] = arr[i] + arr[j];
	arr[j] = arr[i] - arr[j];
	arr[i] = arr[i] - arr[j]; 
}
```



### 例题 1-4：鸡兔同笼题目

已知鸡和兔的总数为n，总腿数为m，输出鸡和兔的数目- 我的解 O\(n\)

```java
public int[] cal (int n, int m)
{ 
    for(int i = 0;i< n;i++)
    {
        int rat = n-i;
        if(4*rat + 2*i == m) return new int[]{i,rat};
    }
    return new int[2];
}
```

书上的解法

```java
public int[] cal (int n ,int m)
{
    int a = 2*n-m/2;
    int b = m/2-n;
    if(m%2 == 1 || a<0|| b<0)
    return new int[]{a, b};
}
```

### 例题 1-5 三整数排序

输入三个整数，从大到小排序后输出 我的解

```java
public int[] sort(int a ,int b,int c)
{
    int[] res  = new int[3];
    if(a<=b && a<=c )
    {
        if(b<=c) return new int[]{a,b,c};
        else return new int[]{a,c,b};
    }
    else if(b<=c && b<=a)
    {
        if(a<=c) return new int[]{b,a,c};
        else return new int[]{b,c,a};
    }
    else if(c<=b && c<=a)
    {
        if(b<=a) return new int[]{c,b,a};
        else return new int[]{c,a,b}
    }
    return res;
}
```

书上的解, 先通过swap来找出最小值，然后找出次小值，最后就能对三个数排序

```java
public int[] sort(int a ,int b,int c)
{
    if(a>b) { int temp = a ; a = b ; b = temp};// now a<=b
    if(a>c) { int temp = a ; a = c ; c = temp};// now a<=c
    if(b>c) { int temp = b ; b = c ; c = temp};// now b<=c
    return new int[]{a,b,c};
}
```

习题

1-6 判断三个整数能否组成三角形

```java
public boolean triangle(int a,int b, int c)
{
    if(a+b<=c) return false;
    if(a+c<=b) return false;
    if(b+c<= a) return false;
    return true;
}
```

1-7 判断输入的年份是否为闰年

```java
public boolean whatYear(int year)
{
    if(year<0) return false;
    if(year%4 == 0)
    {
        if(year%100 != 0) return true;
        if(year%400 == 0) return true;
    }
    return false;
}
```



