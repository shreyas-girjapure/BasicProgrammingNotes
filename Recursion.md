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
