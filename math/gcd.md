# GCD (Greatest commond divisor)

The greatest common divisor (GCD) of two numbers a and b is the greatest number that divides evenly into both a and b. Naively we could start from the smallest of the two numbers and work our way downwards until we find a number that divides into both of them:

```
for (int i=Math.min(a,b); i>=1; i--)
   if (a%i==0 && b%i==0)
      return i;
```

Although this method is fast enough for most applications, there is a faster method called Euclid’s algorithm. Euclid’s algorithm iterates over the two numbers until a remainder of 0 is found.

```
public int GCD(int a, int b)
{
   if (b==0) return a;
   return GCD(b,a%b);
}
```
