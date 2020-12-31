# Bitwise Operational Problem Pickups

## Find if Kth bit is set 

>**Problem**
Given a Number N and Kth bit K , find it the Kth bit is 1 or not

Example:

    Input : 5 , 1
    Output : true

    Input : 8 , 2
    Output : false

Soultion :

    Approach 1: 
    1. Divide the number till K
    2. If Remainder in Kth iteration is 1 return true

Code : 
```java
boolean isSet(int N,int K){
    for(int i = 1 ; i <=K ; i++){
        int rem = N % 2;
        N =N / 2;        
        if(rem==1 && K ==i){
            return true
        }
    }
    return false;
}
```    
    Approach 2:
    Idea: Idea here is to move Kth bit to 1st postition or to Rightmost bit and then multipply it with 1 [0001]
    So now if the Kth bit is 1 and when we AND it with 1 we get 1

    Example :
    N = 5 , K =3;
    5 [ 101 ]
    1 [ 001 ]

    5 & 1 = 001
    so the Kth bit is 1 or set we return true

    Steps:
        1.Right shift N by K-1 [Here theory is when we shift by K-1 the 
        kth bit moves to right most place ]
        2. AND result with 1 
        3. Return true if result is 1 , else false
    
Code:
```java
    public static boolean isSetRightShift(int N , int K){
        return (((N>>(K-1)) & 1)==1);
    }
```

## Count the number of Set bits

>**Problem**
Given an int N count the number of set bits in it

Example:

    Input : 5
    Output : 2

    Input : 7
    Output : 3


Solution:

    Approach 1:
    Get the binary representation of the number and count++ 
    when the N % 2 == 1 

Code:
```java
public static int countSetBits(int N ){
        int count = 0;
        while(N!=0){
            if(N%2!=0){
                count++;
            }
            N=N/2;
        }
    return count;
}
```

    Approach 2 :
    Make all operations with bitwise operators
    N % 2 => N & 1
    N / 2 => N >> 1

    Approach 3 : 
    We can skip the if condition and count++ with 
    count = count + (N & 1)

    Approach 4 :
    ** Brain Kerningam's Algorithm**
    1 0 1 & 1 0 0 = 1 0 0
    Idea: Idea here is When ( N AND N-1 ) results to right most set bit removed

Code : 
```java
    public static int countSetAlgo(int N){
            int count = 0;
        while(N!=0){
            N = N & (N-1);
            count++;
        }
        return count;
    }
```
    Approach 5 :
    ** Look up Table**
    Idea : 
    Idea here is to divide the given 32 bit representation into 8bits

    8bit 8bit 8bit 8bit = 32 bit

    and then make a lookup table for 256 numbers

    We will make an array / lookup table of size 256 to represent 
    each number till 255 [as 8bit can represent only till 255 0-255]

        LookupTable filling :
            1.Here we will start with empty array of size 256 ,
            2.Loop from 1-255 and set the value of number which represents Number
            of set bits in it  
            3. Example for 1 : arr[1] = (1 & 1) + arr[1/2];
            for 5 [1 0 1] : arr[5] = (5 & 1) + arr[2];
            Note : every binary representation is made by dividing number by 2
            So for making a number we use N/2 to use precomputed count:

            5 = (if is odd) + arr[2];
            1 [0 1] in bracketed value which is 2 we have already computed
            value of it , and so on for bigger numbers

        Merging the 8bit values : 
        1. Here we first AND N with 0xff[ all 1s in 8bit ] to get last 8bit representation of the 32bit number 

        32bits of 5
        00000000 00000000 00000000 00000101

        [0000000 00000000 00000000 00000101] & 
        [0000000 00000000 00000000 11111111] = [0000000 00000000 00000000 00000101] (5)

        which is only last 8bits of number others are forced to 0

        2. Now we add result of arr[5] into result and shift the bits to right by 8 
        N>>8 
        this will get us the next 8 bits 
        0000000 00000000 [00000000] 00000101 bracketed ones
        
        We again repeat process of adding 2wice 
        and return the result.

Code:

```java
public static int countSetLookupTable(int N){
    int[] arr = new int[256];
    
    for(int i=1;i<256;i++){
        arr[i] = (i & 1) + arr[i/2];
    }
    int result = 0 ;
    while(N!=0){
        result = result + arr[(N & 255)];
        N= N>>8;
    }
    return result;
}
```

## Power of 2

>**Problem**
For a given interger check if the number is power of 2 or not 


Example : 

    input : 5
    output : false

    input : 4
    output: true

    input : 6
    output : false


Solution :

    Approach 1 : 
    Bruteforce way is to divide number by 2 till 1 
    if we get number as Odd in between return false

    Example : 6 
    6 /2 = 3 => return falsse

    Example : 8 
    8/2 = 4
    4/2 = 2
    2/2 = 1 
    Never got odd return true

    Approach 2 :
    We know that binary rep of power of 2 has only 1 set bit
    If we use Brain kermingam's algo we will get in O(1)

    Approach 3 :
    Idea :
    Here idea is to AND the number with its N-1
    if the number is power of 2 then N-1 would be all 1 except the leftmost
    Example :
    for 8
        8     &     7       = 0
    [1 0 0 0] & [0 1 1 1]   = [0 0 0 0]

    for 6
        6     &     5       = 0
    [0 1 1 0] & [0 1 0 1]   = [0 1 0 0]

Code :

```java
public static boolean isPow2(int N){
    if((N & 1)==1 || N==0){
        return false;
    }
    int newN = (N & (N-1));
    return (newN==0);
}
```
