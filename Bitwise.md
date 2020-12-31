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
    