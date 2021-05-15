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
        Now that you are subtracting why not use better subtraction i.e
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

> **Problem**
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
    2. Loop till a * b
    3. Return number found such that both a and b divides it completely.

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

    Approach 2 :
        Another way is to
        lcm = a * b / gcd(a,b);
        for 4,6
        lcm = 24/2;
        lcm = 12;

## Is Prime

> **Problem**
> For a given number check if it is prime

Example:

    input: 4,
    output : false
    ---
    input : 5 ,
    output : true

Solution :

    Approach 1 :
    1. Run a loop from 2 till the number
    2. Check if i divides number completely
    3. If so return true else false
    4. Corner case for 2 if number is less than 2 return false

    Approach 2:
        Here we use understanding of factor pairs
            consider a number 12
            1, 2, 3, 4, 6, 12 are the factors
            and for every factor there exist a pair number
            2-6 , 3-4 , 12-1
            So some how we need to only check till the Squareroot of N.
            Example : root of 12 = 3
            We check only till 3.
            
        Note : WHY we check till root N 
            Ans : 
            consider number 12 
            it has pairs of 
            1-12 , 2 - 6 , 3-4 
            and if we start calculating pairs from 4
            we get 4-3 , 6-2,12-1
            
            which means after root of n the other number starts declining
            
            example : 
            36 
            6 * 6 = 36
            
            1 * 36 = 36
            2 * 18 = 36
            3 * 12 = 36
            4 * 9 = 36
            6 * 6 = 36
            9 * 6 = 36
            
            we start repeating after root of N
            
            so to check if the extra pair exists we check only till root of N
            
            if there is one more number which can form a pair we return false;

Code :

```java
boolean isPrime(int n){
    if(n ==2 || n===1){
        return false;
    }
    for(int i =2; i*i<=n ; i++){
        if(n%i==0){
            return false;
        }
    }
    return true;
}
```

    Approach 3:
        Skipping some iteration of above code
            If N is large say 1231444
            then root would also be large 1,109
            in such cases we can further reduce the number of iteration
            if we skip the multiples of 2 and 3 then iterations we need
            would be
            1109 - (1109/2 + 1109/3)
            1109 - (554 + 396)
            1109 - 950
            159 So we would only need 159

Code :

```java
boolean isPrime(int n){

    if(n==1) return false;

    if(n ==2 || n==3) return true;

    if(n % 2 || n % 3){
        return false;
    }
    for(int i = 5; i*i<=n ; i=i+6){
        if(n%i==0 || n % (i+2)==0){
            return false;
        }
    }
    return true;
}
```

## Prime factors

> **Problem**
> Given a number N print all prime factors of N

    Example:

    Input: 12,
    Output: 2 2 3

Solution :

    Approach 1 :
    1. Run the loop from 2 to N.
    2. If a number is divisible by i then change the N = N/i
    3. Print the complete divisiors

Code :

```java
public static void primeFactors(int n){
    for(int i=2;i*i<=n;i++){
        while(n % i == 0){
            System.out.println(i+" ");
            n = n / i;
        }
    }
    if(n>1){
        System.out.println(n+" ");
    }
}
```

    Approach 2:
    We can enhance above apporach for handling cases of multiples of
    numbers for example 2 4 6

Code :

```java
public static void primeFactors(int n){
    while(n%2==0){
        System.out.println(2+" ");
        n=n/2;
    }
    while(n%3==0){
        System.out.println(3+" ");
        n=n/3;
    }
    for(int i=5;i*i<=n;i=i+6){
        while(n % i == 0){
            System.out.println(i+" ");
            n = n / i;
        }
        while(n % (i+2) == 0){
            System.out.println(i+" ");
            n = n / (i+2);
        }
    }
    if(n>3){
        System.out.println(n+" ");
    }
}
```

## All divisiors

> **Problem**
> Given a number print all the divisors of the number

    Example:
    Input: 15,
    output : 1, 3, 5, 15

Solution:

    Approach 1 :
    1. Run loop till number
    2. Check if anyone divide the number , if it does print the number

Code:

```java
void allDivisors(int n){
    for(int i = 1 ;i <= n ; i++){
        if(n % i ==0){
            System.out.print(i+" ");
        }
    }
}
```

    Approach 2 :
    We know that divisors are in pair
    i.e  for 15
    if 1 divides it then (1-15)
    if 3 divides it then (3-5)
    and we have to only check till root of n
    [because of pair logic which i dont yet understand but thing is we have to check till root N if we get it we get it]
    1. Run till root of number
    2. Check if number divides if it does print i and n/i - the pair

Code:

```java
void allDivisors(int n){
    for(int i = 1 ;i*i <= n ; i++){
        if(n % i ==0){
            if (i==n/i){
            System.out.print(i+" ");
            }
            else {
            System.out.print(i+" "+n/i);
            }
        }
    }
}
```
    Approach 3 :
    Now that we can print it unordered we will make it ordered by
    traversing till root n and then goin back from root n till 1
    1. Traverse till root n
    2. check for division if it does print it.
    3. Now keeping the root n in variable check form variable to 1 
    4. check if someone divides if it does print the n/i

    Corner case : 
    && (n/i!=i) check this for numbers like 25 5 * 5 we do not want 5 again

Code:

```java
void allDivisors(int n){
    int i = 1 ;
    for(;i*i <= n ; i++){
        if(n % i ==0){           
            System.out.print(i+" ");            
        }
    }
    for(;i>=1;i--){
        if(n % i ==0 && (n/i!=i)){
            System.out.print(n/i+" ");
        }
    }
}
```

## Sieve of Eratosthenes

>**Problem**
Given a number N print all the prime numbers till N (inclusive).

    Example:
    Input:10
    output: 2, 3, 5 ,7 

Solution:

    Approach 1:
    1. Loop till number 
    2. check if i is prime 
    3. Print if true

    Approach 2 :
    1. Take an array of size n+1 [because n+1 would make our life easier in printing]
    2. Run a loop till N
    3. Mark all the multiple of numbers till N in a loop and assign thier value as 0
    4. Repeat the same.
    5. Print all the number with value 1

Code :

```java
void primeTillNumber(int n ){
    int[] arr = new int[n+1];
    for(int i = 2 ; i < arr.length ; i++){
        arr[i] = 1;
    }
    for(int i = 2; i*i<=n ; i++){
        if(isPrime(i)){
            for(int j = 2 * i ; j <=n ; j=j+i ){
                arr[j] = 0;
            }
        }
    }
}
```


    Approach 3:
    Here we are doing some repeat work , we are also marking the multiples of 4 or multiples of 6 which should be skipped as we already marked thier factors
    Consider this case for 35
    we are looping over 
    2, 3 ,4 ,5 as fits under root n
    and for 5 
        We are marking 10,15,20,25,30,35
        Now here 10 should already be marked by 2, 
        15 by 3 , 20 by 2 
        Only 25 needs to be marked by 5 
    So we make inner loop start from square 
    and mover further with multiples

Code :

```java
void primeTillNumber(int n ){
    int[] arr = new int[n+1];
    for(int i = 2 ; i < arr.length ; i++){
        arr[i] = 1;
    }

    for(int i = 2 ; i *i <=n ;i++){
        if(isPrime(i)){
            for(int j = i * i ; j <= n ; j = j + i){
                arr[j] = 0;
            }
        }
    }
    for(int i = 2 ; i < arr.length ; i++){
        if(arr[i]==0){
            System.out.println(i);
        }
    }
}
```

## Computing Power Recursive

>**Problem**
For given 2 numbers a and b find a to the power b.

    Example :
    Input : 2 3 
    Output : 8

Solution:

    Approach 1 :
    For bruteforce 
    1. run loop till b times
    2. Multiply a to self till b times
    3. Return result

Code :

```java
static int pow(int a,int b){
    if(b==0){
        return 1;
    }
    if(b==1){
        return a;
    }
    int res = 1;
    for(int i=0;i<b;i++){
        res = res * a;
    }
    return res;
}
```

    Approach 2 :
    Thing with powers is 
    If power is even then for a, b
        pow(a,b) = pow(a,b/2) * pow(a,b/2)
        pow(2,6) = pow(2,3) * pow(2,3)
        64 = 8 * 8
    If power is odd then for a , b
        pow(a,b) = pow(a,b-1) * a
        pow(2,7) = pow(2,6) * 2
    For even case the RHS terms are equal if we compute one of them we are GOLDEN!


Code :

```java
int pow(int a, int b){
    if(b==1){
        return a;
    }   
    int temp = pow(a,b/2);     
    temp = temp * temp;
    if(b % 2 ==0){        
        return temp;
    }
    else {
        return temp * a;
    }
}
```

## Computing power Iterative

>Problem
Given two numbers find the the power , for a , b find a to the power b

    Example :
    input : 2,3
    output : 8


Solution :

    Approach 1:
    we can represent any number as powers of 2 (binary magic)

    For example 10 can be written as 2^8 * 2^1 
    We use this for our advantage
    for 10 - 1010 
    a = 2 , b =10
    Here for our 1 logic we multiply result with current power of a
    Example : 1 0 [1] 0 for brackated 1 result should be res = 2^2 * 1 , and for other it should be 2^8 * 4

    Some more clearance 
        our a series is 
            2 = 2^1
            4 = 2^2
            16 = 2^4
            256 = 2^8
    
    Algorithm is 
        1. Convert power into binary 
            We keep % number by 2 if it is 0 we take it as MSB 0 rightmost 
            We make N/2 and check again if it is 1 we make MSB 1
        2. for 1 logic we make a * i 

Code :

```java
int pow(int a , int b){
    int res = 1;
    while(b>0){
        if(b % 2 !=0){
            res = res * a;            
        }
        a = a*a;
        a =a / 2;        
    }
    return res;
}
```        
