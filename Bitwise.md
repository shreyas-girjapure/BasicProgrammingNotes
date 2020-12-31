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

    Step