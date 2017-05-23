So what does the base of the number actually mean? We will begin by working in the standard (decimal) base. Consider the decimal number 4325. 4325 stands for 5 + 2 x 10 + 3 x 10 x 10 + 4 x 10 x 10 x 10. Notice that the "value" of each consequent digit increases by a factor of 10 as we go from right to left. Binary numbers work in a similar way. They are composed solely from 0 and 1 and the "value" of each digit increases by a factor of 2 as we go from right to left. For example, 1011 in binary stands for 1 + 1 x 2 + 0 x 2 x 2 + 1 x 2 x 2 x 2 = 1 + 2 + 8 = 11 in decimal. We have just converted a binary number to a decimal. The same applies to other bases. Here is code which converts a number n in base b (2<=b<=10) to a decimal number:

```
public int toDecimal(int n, int b)
{
   int result=0;
   int multiplier=1;
   while(n>0)
   {
      result+=n%10*multiplier;
      multiplier*=b;
      n/=10;
   }
   return result;
}
```

From decibal to another base:

```
public int fromDecimal(int n, int b)
{
   int result=0;
   int multiplier=1;
   while(n>0)
   {
      result+=n%b*multiplier;
      multiplier*=10;
      n/=b;
   }
   return result;
}
```

If the base b is above of 10 than we must use non-numeric characters to represent digits that have a value of 10 and more. We can let ‘A’ stand for 10, ‘B’ stand for 11 and so on. The following code will convert from a decimal to any base (up to base 20):

```
public String fromDecimal2(int n, int b)
{
   String chars="0123456789ABCDEFGHIJ";
   String result="";
   while(n>0)
   {
      result=chars.charAt(n%b) + result;
      n/=b;
   }
   return result;
}
```
