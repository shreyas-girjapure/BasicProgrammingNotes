# Mathematical Problem Pickups

## Count the digits

> **Problem**
> For counting the digits the trick is to divide
> the number by 10 and update the number till number becomes Zero.

    Example:

    Count the number of digits in 345

    1. divide 345 by 10 and count++ `Number: 345 Count : 1`
    1. 34 by 10 and count++     `Number:34 Count:2`
    1. 3 by 10 and count++     `Number:3 Count:3`
    1. Now 3 by 10 is 0 so we stop the loop

## Palindrome Numbers

> **Problem**
> Basic idea is to reverse the numeber and check if the
> reversed number and original number are same

For Example :

Is Number 121 palindrome? `121-true`
Is number 345 palindrome? `345-false`

Solution:

    approach:
    Here basic fix is to consider base result as 0
    and add the reminders in it.

```
0
(0 * 10) +5 = 5
(5 * 10) +4 = 54
(54 * 10) +3 = 543
```

```java
public static int reverseNumber(){
    int res = 0;
    int number = 345;
        while(number!=0){
            int rem = number % 10 ; // 345 % 10=5;
            res = (res * 10) + rem ;
            number = number / 10; // 345 / 10 = 34;
        }
    return res;
}

```

## Factorial of a number

    Idea :
    Factorial of number is the Number multiplied by its
    previous natural number series

`Factorial of 4 : 4 * 3 * 2 * 1 = 24`

```
Input : 4
Output : 24
---
input : 5
output: 120
```

Solution:

    approach:
        1. Itarative :
            Start with result as 1 and
            loop over number till 1 and multiple number with result
        1. Recursive:
            Take base case when number is 0 and return for 0
            for other cases
            return number * f(number-1)

Code:

```java
int factorial(int n){
    int res = 1;
    for(int i = n ; i >=1;i--){
        res= res *i;
    }
    return res;
}
```

Code :

```java
int factorial(int n){
    if(n==0){
        return 1;
    }
    return n * factorial(n-1);
}
```

## Tailing zeroes

**Problem**

    Given a number n find the trailing zeroes of the factorial of the

    input: 5
    output : 1
    --
    input : 10
    output: 2

Solution:

    Approach 1:
    Take factorial of a number and while last reminder is 0 increment count

    Approach 2:
    Catch here is 0 are formed by 5 * 2 ,
    so for 6! there is 5 and 2 involved so fact has 1 trailing 0
    for 10 there is 10 itself and 5 and 2 so 2 trailing 0s
    Case 1:
    20 in 20 we have 4 5s
    Case 2:
    25 in 35 we have 5 5s and extra 5 of 25 i.e 5*5;

Code:

```java
int getTrailingZeroCount(int n){
    int res = 0;
    for(int i = 5 ; i<=n ; i=i*5){
        res = res + n/i;
    }
    return res;
}
```

## GCD or HCF of 2 Numbers

Given 2 numbers find the Greatest Common Divisor or Highest Common Factor between them

    Input: 4 , 6
    output : 2
    Input: 100 , 200
    output : 100

Solution :

    Approach 1:

    The highest of both can not be greater than min(a,b)
    Ex: from 100,200 number more than 100 can not be GCD
    1. Take min of both min(a,b)
    2. Iterate backfrom min(a,b) till 1
    3. If a number is found such that it divides both completly then break and return.

Code:

```java
int gcd(int a , int b){
    int min = Math.min(a,b);
    for(int i = min;i>=1;i--){
        if((a%i ==0) && (b%i==0)){
            return i;
        }
    }
    return 1;
}
```

    Approach 2:
    Euclidian Algorithm
        for a , b
        The gcd is the common divisor of numbers then for g(x,y)
        x and y do not have anything common between them.

        so to get the gcd we subtract bigger number with smaller number
        till both number become equal.

        so finding common basic idea is to subtract till

Code :

```java
int gcd(int a,int b){
    while(a!=b){
        if(a>b){
            a= a-b;
        }else {
            b= b-a;
        }
    }
    return a;
}
```

    Approach 3 :
    Euclidian Division Algo:
        Now that you are subtracting why not user better subtraction i.e
        DIVISION

Code :

```java
int gcd(int a, int b){
    int min = Math.min(a,b);
    while(a%b!=0 || b % a!=0){
        a = a % b;
        b = b % a;
    }
    return Math.min(a,b);
}
```

    Approach 4 :
    Euclidian Division Algo Recursive and Swap Protected:
        Here idea is to return the smallest of both ,
        using mod the value of right is always less than of left.

Code :

```java
int gcd(int a, int b){
    if(b==0){
        return a;
    }
    return gcd(b,a%b);
}
```

## LCM of Two Numbers

> Problem
> Given two numbers find the LCM

    Example:
    input: 4 , 6
    output : 12
    ---
    input : 100, 200
    output : 200
    ---
    input : 2, 8
    output : 8

Solution :

    Approach 1 :
    For brute force we can start with consideration ,
    Min ans would be Max of both numbers i.e between 2 ,8 it has to be
    greater than or equal to 8 ,
    Example 6 would not be in table of 8.
    1. Take Max of a, b
    1. Loop till a * b
    1. Return number found such that both a and b divides it completely.

Code :

```java
int lcm(int a,int b){
    int max = Math.max(a,b);
    for(int i = max;i<=a*b;i=i+max){
        if(i % a==0 && i % b==0){
            return i;
        }
    }
    return a*b;
}
```
