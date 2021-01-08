# Recursion Problems

## Print N to 1 using recursion

>**problem**
Given a number N print all the numbers till 1

Example :

    Input : 4
    Output : 4 3 2 1

Solution :

    Base Condition :
        if(n==0){
            return 0;
        }

    statements:
    System.out.println(n);

    Calls : 
    printTillOne(n-1);


Code : 

```java
public static void printTillOne(int n){
    if(n==0){
        return ;
    }
    System.out.println(n);
    printTillOne(n-1);
}
```


## Print 1 to N using recursion

>**problem**
Given a number N print all the numbers from 1 to N

Example :

    Input : 4
    Output : 1 2 3 4

Solution : 

    Base Condition :
        if(n==0){
            return 0;
        }

    statements:
    System.out.println(n);

    Calls : 
    printTillOne(n-1);


    Here notatble thing is to print number later and inner call first 

    as we have to start from lower end , we have to first reach to lower 
    end and then start printing.

    with this logic we have printed after call finishes.


Code :

```java
public static void printTillOne(int n){
    if(n==0){
        return ;
    }
    printTillOne(n-1);
    System.out.println(n);
}
```

## Palindrome check usinig recursion

>**problem**
Given a string S check if string is palindrome ?


Example:

    Input : "121"
    output : true

    Input : "1221"
    output : true

    Input : "1214432"
    output : false


Solution :

    Idea :
    Recursive way of doing things here would be 

    1. Compare first and last characters 
    2. if they are same.
    3. check for smaller problem.    
    4. Repeat

    Base case : 

    if(String.length==0 || String.length==1){
        return true;
    }

    Here 2 base cases are handled 

    1. "" empty string => which we consider as palindrome
    2. "b" Single character => which is also palindrome

    Now after checking for first and last charecter we pass smaller 
    string to our function

    if any case fails we get false and when we AND false with true/false 
    we will get return as false

    This way we can RECURSIVELY find the ans

Code : 
```java
public static boolean isPalindrome(String s){
    if(s.length()==0 || s.length()==1){
        return true;
    }
    return (s.charAt(0)== s.charAt(s.length()-1)) && 
    isPalindrome(s.substring(1,s.length()-1));
}
```    

```java
//One more way to write same solution is to use start and end 
//to keep things simple
// Here base case is that we do not want to cross our start and end indexes
// For example     
    // "abbc" 
    // Here we will stop checking when start =1 , end = 2; , 
    //as in our next iteration start =2 ,and end = 1;
    //which we have already computed so we will stop when 
    // start > end

public static boolean isPalindrome(String s , int start,int end){
    if(start > end){
        return true;
    }
    return (s.charAt(start)==s.charAt(end)) && isPalindrome(s,start+1,end-1);
}
```

## Natural number sum

>**problem**
Given a number N print the sum of all natural numbers upto N

Example :

    Input : 5
    Output : 15

    Input : 3 
    Output : 6

Solution :

    for 3 
    3 + 2 + 1

    for 5 
    5 + 4 + 3 + 2 + 1

    so if we think about smaller sub problem 

    5 + sum(4);

    and BASE CASE : 
    if(n==0){
        return 0;
    }

Code :

```java
public static int sumTillN(int n){
    if(n==0){
        return 0;
    }
    return n + sumTillN(n-1);
}
```

## Sum of number N 

>**Problem**
Given a number N find sum of its digits


Example : 
    
    Input : 234
    Output : 9 [2 + 3 + 4]

    Input : 33
    Output : 6 [3 + 3]

    Input : 3
    Output : 3 

Solution :

    Here we already know a mathematical trick 

    Get last digit of a Number 
        Take Mod % 10
        Example :
            123 % 10 = 3;
        
    Get Number - 1 digit number
        Divide number by 10
            Example :
                123 / 10 = 12
    
    This way we can get smaller subproblems 

    for 234 
        4 + 3 + 2

        we can start with 4 + Sum(23) ;

        which can be done by (N % 10) + sum(234 / 10)

Code : 
```java
public static int sumOfNumber(int n){
    if(n==0){
        return 0;
    }
    return (n % 10) + sumOfNumber(n / 10);
}
```

## Rope cutting problem 

>**Problem**
For given N , a ,b ,c 
Find number of possible cuts of N sized rope
Return -1 if no case exist

Example :

            N a b c
    Input : 5 2 5 1
    output : 5

    Here we can cut 5 sized rope in 5 pieces into c sized rope
            N a b c
    Input : 23 11 9 12
    Output : 2

    Here we can cut 23 sized rope in 2 pieces with 11 
    23 -11 = 12 
    12 - 12 = 0

    if we try to cut it with 9 we do not get remaaining size equal to 
    a or b or c

Solution :

    Here important thing is to think of a sub problem and to figure out a 
    base case where we would stop.

    For our example :

    23 11 9 12

    We have to cut 23 with all the sized ropes 
    example , 

    [23 - 11] , 23 - 9 , 23 -12 

        
    for [23-11] example we will proceed first 

    23 - 11 => 12 

    Now we again cut result with all a b c

    [12 - 11] , 12 - 9 , 12 - 12            **

    12 -11 => 1

    Now we again cut the result with all a b c

    [1 - 11] , [1-9] , [1-12]

    Here we note that if result gets negative it is of NO USE
    So we will return -1 here ,

    12 - 11 , 12 -9 , 12-12

    Here we get 12 - 12 when we get result as 0 , that indicates we have 
    completely divided rope with a possible combination

    So we will return the depth ,


    We will collect depths of all possible subproblems and find the 
    maximum among them.


Code :
```java
public static int numberOfRopeCuts(int n  ,int a , int b , int c, int depth){
    if(n<0){
        return -1;
    }
    if(n==0){
        return depth;
    }
    int aRes = numberOfRopeCuts(n-a,a,b,c,depth+1);
    int bRes = numberOfRopeCuts(n-b,a,b,c,depth+1);
    int cRes = numberOfRopeCuts(n-c,a,b,c,depth+1);
    
    return Math.max(Math.max(aRes,bRes),cRes);
}
```


##Generate Subsets

>**Problem**
Given a string , Generate its powerset OR sub sequences.


Example :

    Input : "ab"
    Output :  a b ab

    Input : abc
    Output :  a b c ab ac bc abc


Solution :
    [Link to solution](https://ide.geeksforgeeks.org/TKC8QoVRiy)

    There is iterative solution availble , but here we are discussing Recursive

    There is pattern in subsequence problem 
    
                            ""
                    ""               a              => choice of a
                ""      b       a        ab         => choice of b
            ""     c  b   bc  a   ac   ab   abc     => choice of c


    In the first level there is choice of adding "a" and not adding "a"
    0 1

    In next level there is choice of adding "b" and not adding "b"

    00 01 10 11

    In next level there is choice of adding "c" and not adding "c"

    [000 001] 010 011 100 101 110 111

    Consider bracketed pair 

    for 00

    there exist 2 pairs either with 1 at end or wiht 0 at end

    000
    001

    Same thing forms subsequences

    if we observe closely there are only 2 calls , 
        1. Not add anything at end
        2. Add something at end
    
    and for our base case we will stop when depth == s.length()


Code :
```java
// main call 
//  generateSubsequence("abc","",0);

// Here we start with "" empty string and go in depths of it with 
//appending to it.

public static void generateSubsequence(String s,String current,int depth){
    if(depth == s.length()){
        System.out.println(current);
        return;
    }
    generateSubsequence(s,current,depth+1);
    generateSubsequence(s,current + s.charAt(depth),depth+1);
}
```    


## Tower of hanoi

>**Problem**
Given N print all the steps to move all disks from A to C

Rules : 
        You can only move one disk at a time
        Larger sized disk cannot be kept on smaller disk.

Example :

    Input :2 

    Output:
    Move disc 1 from A to B 
    Move disc 2 from A to C
    Move disc 1 from B to C

    Input :3

    Output:
    Move disc 1 for A to C
    Move disc 2 from A to B
    Move disc 1 from C to B
    Move disc 3 from A to C
    Move disc 1 from B to A
    Move disc 2 from B to C
    Move disc 1 from A to C

Solution :
[Link to solution](https://ide.geeksforgeeks.org/AyANwHHGzx)
[Link to Video](https://www.youtube.com/watch?v=l45md3RYX7c&list=PL_z_8CaSLPWeT1ffjiImo0sYTcnLzo-wY&index=11)

    Here we use a approach for solving recursion problem known as 
    
                Induction BaseCondition Hypothesis
    
    Hypothesis :
    towerOfHanoi(n) => Would shift all my plates to destination plate

    is the hypothesis

    For N =3 

    We first need to shift all the N-1 plates to Another pole
    and then we can simple move the last plate to final destination

    so hypothesis for our function 
    towerOfHanoi(n , source , destination , helper) is => 

    this would shift all the plates from source to destination

    Now for N-1 plates to be shifted to another pole , 
    we need to pass N-1 to function and change the destination

    then our task would be completed of shifting N-1 to destination



    for that we say 
    towerOfHanoi(n-1,A,B,C)

    and 3rd plate [only remaining plate] needs to be shifted to C

    to solve that we print
    "Move n from A to C"

    and then all the N-1 plates from B needs to be finally shifted from B to C

    So

    towerOfHanoi(n-1,B,C,A)

    Base Condition :

    We stop when there is only 1 plate left 
    if(n==1){
        print(Move n from source to destination);
        return;
    }


Code : 
```java
public static void towerOfBramha(int n , char src , char dest , char helper){
    if(n==1){
        System.out.println("Move "+ n + " from "+ src+" to "+dest);
        return;
    }
    towerOfBramha(n-1,src,helper,dest);
    System.out.println("Move "+ n + " from "+ src+" to "+dest);
    towerOfBramha(n-1,helper,dest,src);
}
```

## Josephus problem

>**Problem**
Given integer N and integer K , for N persons standing in a circle,Kill
the kth person from 0 and return the only remaining surviour.

Example :

    Input : 5 2
    Output : 2

    0 1 2 3 4
    0 [1] 2 3 4
    0 [1] 2 [3] 4
    [0] [1] 2 [3] [4]

Solution :
[Link to solution](https://ide.geeksforgeeks.org/FstqmR0j7X)
[Link to Video](https://www.youtube.com/watch?v=ULUNeD0N9yI)
[Link to Video 2](https://practice.geeksforgeeks.org/tracks/DSASP-Recursion/?batchId=155)


Code : 
```java
class GFG {
    
    public static void josephusProblem(ArrayList<Integer> arr,int k,int index){
        if(arr.size()==1){
            System.out.println(arr.get(0));
            return;
        }
        index = (index +k-1) % arr.size();
        arr.remove(index);
        josephusProblem(arr,k,index);
    }
    
    public static void main (String[] args) {
        int n = 5;
        int k = 2;
        ArrayList<Integer> li = new ArrayList<Integer>();   
        for(int i=1;i<=n;i++){
            li.add(i);
        }
        int index = 0;     
        josephusProblem(li,k,index);
    }
}
```

## Kth grammer Problem

>**Problem**
On the first row, we write a 0. Now in every subsequent row, we look at the previous row and replace each occurrence of 0 with 01, and each occurrence of 1 with 10.
Given row N and index K, return the K-th indexed symbol in row N. (The values of K are 1-indexed.) (1 indexed).


Example :

    Input: N = 1, K = 1
    Output: 0

    Input: N = 2, K = 1
    Output: 0

    Input: N = 2, K = 2
    Output: 1

    Input: N = 4, K = 5
    Output: 1

    Explanation:
    row 1: 0
    row 2: 01
    row 3: 0110
    row 4: 01101001


Solution :
[Link to solution](https://leetcode.com/problems/k-th-symbol-in-grammar/)
[Link to Video](https://www.youtube.com/watch?v=5P84A0YCo_Y)

    The problem can be solved by IBH method with a Hypothesis and a base case

    Base case : 
    Base case is given in problem statement i.e if(n==1 && k==1) return 0;


    Then 
    Hypothesis kthGrammer(int n , int k) will return the desired Kth element

    Induction :
    here there is a pattern to note in Nth row and N-1 row

    N rows
    1   0
    2   01    
    3   0110
    4   01101001

    half bits are same and other half are inverted 

    for 3 and 4
    3   0110
    4  [0110][1001]
        same  inverted

    so 4 values can be calculated by 3

    Now there is one more problem of reducing K

    if(k<=mid){
        kthGrammer(n-1,k);
    }
    else{
        kthGrammer(n-1,k-mid)==0?1:0;
    }

    Here if K lies in mid or is equal to mid 
    we can simple return K of previous problem

    but if K is greater than mid 
    we have to calculate new K

    that will correspond to previous problem K

    and we will invert that 

    K = K - mid;

    so if K is 5  and for mid 4
    we will get new K 1
    5 4 => 1
    6 4 => 2
    7 4 => 3
    8 4 => 4
Code : 
```java
public int kthGrammar(int N, int K) {
    // N 
    // 1  0 
    // 2  01 
    // 3  0110
    // 4  01101001
    if(N==1 && K==1){
        return 0;
    }
    int size = 1<<N-1;
    int mid = size / 2;
    if(K<=mid){
        return kthGrammar(N-1,K);    
    }
    else{
        return kthGrammar(N-1,K-mid)==0?1:0;                
    }
    
}
```

## Print Permutations

>**Problem**
For a given string s , Print all permutaions of the string

Example :

    Input : ab
    Output : ab ba

    Input : abc
    Output : abc acb bac bca cab cba

Solution :
[Link to solution](https://practice.geeksforgeeks.org/tracks/DSASP-Recursion/?batchId=155)


Code : 
```java
public static String swap(String s,int i,int j){
    String nString = "";
    char[] arr = s.toCharArray();
    char temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
    for(char c : arr){
        nString+=c;
    }
    return nString;
}

public static void stringPermutations(String s , int i ){
    if(i==s.length()-1){
        System.out.println(s);
        return;
    }
    for(int j = i; j < s.length() ; j ++){
        s = swap(s,i,j);
        stringPermutations(s,i+1);
        s = swap(s,j,i);
    }
}
```