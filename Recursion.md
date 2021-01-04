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
    //which we have already computed so we will only compute till
    // start > end
public static boolean isPalindrome(String s , int start,int end){
    if(start > end){
        return true;
    }
    return (s.charAt(start)==s.charAt(end)) && isPalindrome(s,start+1,end-1);
}
```

    
