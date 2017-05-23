Fractional numbers can be seen in many problems. Perhaps the most difficult aspect of dealing with fractions is finding the right way of representing them. Although it is possible to create a fractions class containing the required attributes and methods, for most purposes it is sufficient to represent fractions as 2-element arrays (pairs). The idea is that we store the numerator in the first element and the denominator in the second element. We will begin with multiplication of two fractions a and b:

```
public int[] multiplyFractions(int[] a, int[] b)
{
   int[] c={a[0]*b[0], a[1]*b[1]};
   return c;
}
```

Adding fractions is slightly more complicated, since only fractions with the same denominator can be added together. First of all we must find the common denominator of the two fractions and then use multiplication to transform the fractions such that they both have the common denominator as their denominator. The common denominator is a number which can divide both denominators and is simply the LCM (defined earlier) of the two denominators. For example lets add 4/9 and 1/6. LCM of 9 and 6 is 18.

```
public int[] addFractions(int[] a, int[] b)
{
   int denom=LCM(a[1],b[1]);
   int[] c={denom/a[1]*a[0] + denom/b[1]*b[0], denom};
   return c;
}
```

Finally it is useful to know how to reduce a fraction to its simplest form. The simplest form of a fraction occurs when the GCD of the numerator and denominator is equal to 1. We do this like so:

```
public void reduceFraction(int[] a)
{
   int b=GCD(a[0],a[1]);
   a[0]/=b;
   a[1]/=b;
}
```
