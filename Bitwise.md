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

    Major reason behind this is :
    Power of 2 numbers only have 1 set bit ,
    and we know that if we have to unset right most set bit ,
    We simply AND it with N-1.

    Doing so if we still have a bit in result then it is definately not
    power of 2.

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

## Find the odd occuring number 

>**Probem**
Given set of numbers , find the number which is repeating itself odd times.

Exmaple :

    input : [4 4 3 2 2 2 2]
    output : 3

    input : [8 7 7 8 8]
    output : 8

Solution :

    Approach 1 ;
    Bruteforce way is to pick one number and count its existence in 
    given set if it is odd we return it

    Approach 2: 
        Idea:
            Here major idea is to Use XOR
            XOR has some interesting properties
            4 ^ 0 = 0
            4 ^ 3 = 3 ^ 4
            4 ^ 4 = 0
        So when we xor number with itself we get result as 0 ,
        Now if we XOR all the numbers we will cancel even pairs and 
        the result would be the odd paired number.
    
Code: 
```java
public static int getOddPairedNumber(int[] arr){
    int res = 0;
    for(int i = 0 ; i <arr.length;i++){
        res = res ^ arr[i];
    }
    return res;
}
```    

## Find the missing number 

>**Problem**
Given the set of numbers from 1 to N+1 , Find the missing number.
We are guarenteed that every number is unique.

Exmaple :

    input : [1 3 4]
    output : 2

    input : [1 5 3 2 ]
    output : 4

Solution :

    Approach 1 ;
    Bruteforce way is to use MATHS
        1.Simply take sum till N+1  
        2.Add all the numbers from array
        3. Subtract Sum(N+1) - Sum(arr)
        4. return the result

Code:
```java
public static int missingNumber(int[] arr){
    int sum = 0 ;
    int sumTillRange = ((arr.length+1) * (arr.length+2))/2;
    for(int i = 0 ; i < arr.length ; i++){
        sum=sum+arr[i];
    }
    return sumTillRange - sum;
}
```
    Approach 2: 
        Idea:
            Here idea is to do mathematical stuff like above but with XOR
        1. Take XOR of all the elements in array
        2. Take XOR till N+1
        3. XOR above two
        4. Return the result            
    
Code: 
```java
public static int missingNumber(int[] arr){
    int xResult = 0;
    int sumXResult = 0 ;
    for(int i = 0 ; i <arr.length;i++){
        res = res ^ arr[i];
    }
    for(int i = 1 ; i <= arr.lenght+1;i++){
        sumXResult = sumXResult + i;
    }
}
```

## Find the two odd appearing numbers

>**Problem**
Given the set of numbers , Find the number which appears odd times.
We are guarenteed that there are two odd appearing numbers

Exmaple :

    input : [ 1 1 3 4 4 6 6 6 6 8 ]
    output : 3 8

    input : [4 4 5 5 5 6 6 9 ]
    output : 5 9

Solution :

    Approach 1 ;
    Bruteforce way is to use two for loops and count their existence         

Code:
```java
public static void twoOdds(int[] arr){
    for(int i = 0 ; i < arr.length ; i++){
        int count = 0;
        for(int j = 0 ; j < arr.length; j++){
            if(arr[i]==arr[j]){
                count++;
            }
        }
        if(count % 2 != 0 ){
            System.ut.println(arr[i]);
        }
    }
}
```
    Approach 2: 
        Idea:
           Here idea is to take XOR of all the numbers from array,
           Then result will have the XOR of the odd 2 numbers

           Example :        
           [ 1 1 3 4 4 6 6 6 6 8 ]
           after even repeating numbers cancel each other 
           => 3 ^ 8  => 0 0 1 1 ^ 1 0 0 0 => 1 0 1 1 => 11[decimal]
        Now we have to extract our numbers from this result 
        ---
        Here comes the main XOR magical theory 

        We only get 1 as bit in XOR when there of the bit is 0 
        1 ^ 0 => 1  OR 0 ^ 1 => 1        

        So here we will find all the numbers from our array that have 
        last set bit as 1 
        
        and again we will find all the numbers from our array that have 
        last set bit as 0

        Dividing our array in 2 groups based on last set bit.
        ---
        How to find last set bit ?

            We know that 
            N & N-1 => turns off the last set bit 
            [1 0 1 1]        
          & [1 0 1 0]
          =>[1 0 1 0]
          If we Invert the result we get
          =>[0 1 0 1]

          And after AND with original number we get last set bit back

          [1 0 1 1]
        $ [0 1 0 1]
        =>[0 0 0 1]

        in general N & ~(N-1)
        gives last set bit number
        ----
        Dividing the array , for dividing array we simply AND arr[i] 
        with  our lastSetBitNum

Code: 
```java
public static void twoOdds(int arr[]){
    int xorRes = 0;
    int resOne=0;
    int resTwo=0;
    
    for(int i = 0 ; i < arr.length ; i ++){
        xorRes = xorRes ^ arr[i];
    }
    int lastSetNum = (xorRes & (~(xorRes-1)));
    for(int i = 0 ; i < arr.length ; i++){
        if((arr[i] & lastSetNum )!= 0){
            resOne = resOne ^ arr[i];
        }
        else {
            resTwo = resTwo ^ arr[i];
        }
    }
    System.out.println(resOne);
    System.out.println(resTwo);
}
```

## Power Set 

>**Problem**
Given a string generate a power set of its characters


    Input : "ab"
    Output : "" , "a" ,"b" ," ab"


Solution :

    Approach :

    There are major 2 steps 
    1. Iterate till 2^size
    2. check which bit is set in the iteration number
        a. Run an inner loop till size
        b. check for 0-size if the bit is set.
            How to check if bit is set?
                1<<i [shift bit i times] do AND with iteration number
    
Code:
```java
public static List<String> allSubsets(String s){
    int size = s.length();
    int total = 1<<size;
    List<String> sets = new ArrayList<String>;
    for(int count = 0 ; count < total ; count++){
        String str = "";
        for(int j = 0 ; j<size;j++){
            if((count & (1<<j))!=0){
                str = str + s.charAt(j);
            }
        }
        sets.add(str);
    }
    return sets;
}
```


## Calculate square without using  / * % pow()

>**Problem**
Given integer return its square

Example :

    Input: 2
    Output: 4

    Input: 3
    Output: 9

Solution :

    Approach : 
        Bruteforce is to use ADDITION
        Add the number N times

Code :
```java
public static int square(int n){
    int result = 0 ;
    for(int i=1 ; i<=n ; i++){
        result = result + n;
    }
    return result;
}
```

    Approach 2 :
        Another way is to use MATHS 
            for even numbers
            ex:
                6 => 4 * square(6/2);
                8 => 4 * square(8/2);
            in general 
                for even number X
                X => (2 * (X/2))
                    => square(2) * square(X/2)
                
                for odd number Y
                Y => square(Y-1+1)
                Here (Y-1) is definately even 

                finally for odd
                square(a+1) = square(a) + 2(a) + 1
                square(Y-1) + 2(Y-x) + 1


## Calculate quotioent without using * / % operators

>**Problem**
Given integer N and divisor D return its quotient

Example :

    Input: 10 3
    Output: 3

    Input: 10 5
    Output: 2

Solution :

    Approach :
        One way is to subtract number till N >= D

Code :
```java
public static int getQuotient(int n , int d){
    int count = 0;
    while(n>=d){
        n=n-d;
        count++;
    }
    return count;
} 
```        

    Appraoch 2 :
    there is another apporach but we dont understand it yet,


## Count set bits till range N

>**problem**
Given number N find total number of set bits till the range

Example :

    Input : 4 ,
    output : 5 

    As 0000 0001 0010 0011 0100 there are total 5 1s till 4

Solution :

    Summery : there are many approches for this problem that we already 
    know    
    but below is interesting way to calculate in O(logN ) time 


    Approach :

    We calculate in chunks here lets calculate for 10

    0000
    0001
    0010
    0011
    0100
    0101
    0110
    0111
    1000
    1001
    1010

    if we calculate manually , there are 17 1s

    Now if we look closely there is fixed calculation pattern for 
    counting set bits till power of 2

    for 8 

    0000
    0001
    0010
    0011
    0100
    0101
    0110
    0111
    
    left most row is 0 , and other rows have equal number of 1s

    this same thing can be said for 4 [as 4 is also power of 2]

    0000
    0001
    0010
    0011

    left most 2 rows are 0 and remaining have equal number of 1s

    Now again going back for our example of 8

    we can say that there are 4 + 4 + 4 = 12 number of 1s till 8[exclusive]

    and for 4 there are 2 + 2 = 4 number of 1s till 4[exclusive]

    for 8 
    pow(2,3) = 8 
    so 
    pow(2,2) * 3

    for 4
    pow(2,2) = 4 
    so
    pow(2,1) * 2

    total bits = pow(2,(logBase2(n)-1)) * logBase2(n)
    are the total bits till power of 2

    Now again coming back to our exaample of 10

    0000
    0001
    0010
    0011
    0100
    0101
    0110
    0111        7
    -------
    1000        8
    1001
    1010        10

    Now that we have calculated till 7 we have to calculate remaining 

    Our remaining numbers have leftmost bit as set 

    so we will add them first to make problem smaller

    [1]000
    [1]001
    [1]010

    we can simply calculate remaining number by (n-[pow(2,3)-1])
    Here in our case 10 - 7 = 3

    So now we have total of 
    bitsTillPowerOf2 + leftMostSetBits

    Now for remaining part 

    1000
    1001
    1010 
    
    and we have already calculated left most 1s

    000
    001
    010             => 2

    the problem gets smaller 

    now we recursively calculate for 2
    and base condition to stop recursion is 
    if(n==0){
        return 0
    }

    and return the result


Code : 
```java
public int countSetBitsTillN(int n){
    if(n==0){
        return 0;
    }
    int result = 0;
    int logBaseTwoOfN = (int)(Math.log(n)/Math.log(2));

    int setBitsTillLog = (1<<(logBaseTwoOfN-1)) * logBaseTwoOfN;

    int leftMostOnes = (n-(1<<(logBaseTwoOfN)))-1; 

    result =  setBitsTillLog + leftMostOnes 
    + countSetBitsTillN((n-(1<<logBaseTwoOfN)));
    
    return result;
}
```


## Number is sparse or not 

>**problem**
Given a number return if number is sparse or not 

Numebr is said to be sparse if it does not have consecutive 1's;


Example :
    Input : 2
    output : true

    0010
    there are no two consecutive 1s

    Input : 3
    output : false

    0011
    there are consecutive 1s

Solution :

    Idea here is to shift number by 1,
        if there are 2 consecutive 1s then AND ing them would result in non 0
        if there are no consecutive 1s AND would be 0

Code :
```java
public static boolean isSparse(int n){        
    return ((n & (n<<1))==0)?true:false;    
}
```

## Longet Consecutive 1s
>**problem**
Given a number return number of longest consecutive 1s

Example :
    Input : 7
    output : 3

    111
    there are three consecutive 1s

    Input : 14
    output : 3

    1110
    there are 3 consecutive 1s

Solution :

    Idea here is to right shift number by 1 ,
        if there are consecutive 1's we will have & as non 0
            also right shift N >>1 in every iteration        

Code :
```java
public static int maxConsecutiveOnes(int x) {
    int count =0 ;
    while(x!=0){
        x=(x & (x>>1));
        count++;
    }
    return count;
}
```