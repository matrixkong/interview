# 第二章 循环

提示 2-3 特别留意**当前行**的**跳转**和**变量**的**改变**

提示 2-4 尽量**缩小变量**的**定义范围**

### 例题 2-1 aabb 输出所有形如aabb的4位完全平方数

```java
public List<Integer> format()
{
    List<Integer> res = new ArrayList<>();
    for(int a = 1;a<10;a++)
    {
        for(int b = 0;b<10;b++)
        {
            //非常巧妙的用 a*1100 + b*11 来得到数字
            int cur = a*1100+ b*11;
            //书上用 Math.floor(cur+ 0.5) 来解决double计算的误差问题
            int floor = (int)Math.floor(Math.sqrt(cur)+0.5); 
            //在java 中有 round 函数可以
            int floor = (int)Math.round(Math.sqrt(cur));
            //记得数据类型转换的问题 double -> int ， int -> double
            if( floor*floor == cur) res.add(cur);
        }
    }
    return res;
}
```

double 计算精度问题 ：如果在计算后 1 变成了 0.99999999, floor的结果是0 而不是 1， 为了减小误差我们改为四舍五入 这样 floor\(x+0.5\)  ==1 x的值范围就从 【1～2）\(floor\(x\) ==1\) 变为【0.5 ~ 1.5\) \(floor\(x+0.5\)  ==1\) 达到了四舍五入的效果

在java 中 提供了 **Math.round** 函数 可以自动为我们**四舍五入**，但是要注意返回的类型是**long**

另外一个思路是枚举法，遍历所有的数字来检测

```java
public List<Integer> format()
{
    List<Integer> list = new ArrayList<>();
    for(int i = 1;;i++)
    {
        int cur = i*i;
        if(cur<1000) continue;
        if(cur>=10000) break;
        if(cur/1000 == (cur/100)%10 && (cur%100)/10 == (cur%10))
            list.add(cur);
    }
    return list;
}
```

提示 for 的三个部分都可以省略

### 例题 2-2 3n+1 的问题 对于任意大于1的自然数 n，如果n为奇数，把n设为 3n+1， 如果是偶数，就设为n的一半，n&lt;=1e9

3-&gt;10-&gt;5-&gt;16-&gt;8-&gt;4-&gt;2-&gt;1

```java
public boolean check(int n)
{  
    long count = 0;
    for(long i = n;i>1;)
    {
        if(i%2 == 0) i>>=1;
        else i= 3*i+1;
        count++;
    }
    return count;
}
```

### 例题 2-3 近似计算 pi／4 = 1 - 1／3 + 1／5  - 1／7 +..... 最后一项小于1e-6

```java
public double cal()
{
    double res = 0;
    for(int i =0;;i++)
    {
        double cur = 1.0/(i*2+1);
        if(cur<1e-6) break;
        if(i%2 == 0) res+=cur;
        else res -=cur;
    }
    return res;
}
```

