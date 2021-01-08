# Random notes

## IBH Recursion Method

[Video Explanation](https://www.youtube.com/watch?v=Xu5RqPdABRE&list=PL_z_8CaSLPWeT1ffjiImo0sYTcnLzo-wY&index=3)
[Video Explanation 2](https://www.youtube.com/watch?v=qDJJBZAIXIw&list=PL_z_8CaSLPWeT1ffjiImo0sYTcnLzo-wY&index=4)
    In this method we make problem simple by defining a hypothesis for our funtion
    Then define a Induction step 
    then write a base case

    Most Recursion problems can we solved by this method easily

    Hypothesis :
    
    Hypothesis step is assuming our function is returning correct output 
    [ even though we have not written anycode for it JUST ASSUME]

    And make problem smaller

    Induction :

    In this step we write for remaining problem

    Base case :

    We write a base case to stop recursion for our function
    Base case is smallest valid subproblem/input


    For example :

    Print all the numbers from 1 to N

    Hypothesis :

    void printTillN(int n) = > will print all the numbers from 1 to n;

    so if we call 

    printTillN(4) 

    output will be 

    => 1 2 3 4

    Now , we run the hypothesis for smaller problem

    printTillN(4-1) = > 1 2 3

    Now between original call and smalller input call 4 is missing 

    and base case would be if(n==1) print(1)

Code :
```java
static void printTillN(int n){
    //base case
    if(n==1){
        System.out.println(n);
    }
    //Hypothesis
    printTillN(n-1);
    //Induction
    System.out.println(n);
}
```

