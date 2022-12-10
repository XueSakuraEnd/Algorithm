# Find the greatest common divisor

## Common algorithm

```c++
for(int i=2;i<=(a>b?a:b);i++){
    int c=i;
    while(a%i==0 && b%i==0){
        c=c*i;
        a=a/i;
        b=b/i;
   }
}
```

## Euclidean algorithm

- A=B*C+D

- GCD（A，B）= GCD（B，D）

- Prove:

> (1)设A=a*k,B=b*k,其中a,b为整数,则D=(a-bC)*k,(a-b*C)为整数
> 所以B与D的最大公约数k等于B与A的最大公约数k
> (2)设B=bk,D=dk,其中b,d为整数,则A=(bC+d)k,(bC+d)为整数
> 
> 所以B与A的最大公约数k等于B与D的最大公约数k

![](https://cdn.jsdelivr.net/gh/XueSakuraEnd/Picgo/Source/202212102041814.gif)

```c++
while(B!=0){
    r=B;
    B=A%B;
    A=r;
}
```

## Stein algorithm

- 更相减损术:
  
  > gcd(a,b)=gcd(b,a-b)
  > 
  > 1.先判断两个数的大小，如果两数相等，则这个数本身就 是就是它的最大公约数。  
  > 
  > 2.如果不相等，则用大数减去小数，然后用这个较小数与它们相减的结果相比较，如果相等，则这个差就是它们的最大公约数，而如果不相等，则继续执行2操作。

- Stein算法:
  
  > 1.当a和b均为偶数，gcd(a,b) = 2gcb(a/2, b/2) = 2gcd(a>>1, b>>1)
  > 
  > 2.当a为偶数，b为奇数，gcb(a,b) = gcd(a/2, b) = gcd(a>>1, b)
  > 
  > 3.当a为奇数，b为偶数，gcd(a,b) = gcd(a, b/2) = gcd(a, b>>1)
  > 
  > 4.当a和b均为奇数，利用更相减损术运算一次，gcb(a,b) = gcb(b, a-b)， 此时a-b的结果必然是偶数，又可以继续进行移位运算。
  
  ```c++
  int gcd(int a,int b){
      if(a==0)
          return b;
      else if(b==0)
          return a;
      if(a%2==0 && b%2==0)
          return 2gcd(a>>1,b>>1);
      if(a%2==0 && b%2!=0)
          return gcd(a>>1,b);
      if(a%2!=0 && b%2==0)
          return gcd(a,b>>1);
      if(a%2!=0 && b%2!=0)
          return gcd(min(a,b),abs(a-b);
  }
  ```
