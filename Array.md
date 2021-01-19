# Array Notes


## Move Zeroes to end


>**problem**
Given array move all 0 to the begining of array



Example :

    Input : 10 0 20 30 0
    Output : 10 20 30 0 0

    Input : 0 0 10 20
    Output : 10 20 0 0

Solution :
[Link to video](https://practice.geeksforgeeks.org/tracks/DSASP-Arrays/?batchId=155)

    Here thinking of the best case ,

    10 20

    Here everything is as we wanted.

    now there are 2 cases here 

    10 20 0 - a zero comes next

    10 20 50 - a non zero comes next

    in case zeero comes next we are good as this is 
    desired o/p

    in case a Non zero comes then we have to attach it to
    the end of line

    i.e after 10 20 -here

    example :

    10 20 0 0 60

    now for 60 we will move 60 to the end of good number
    [numbers which are in desired order] line

    10 20 [60] 0 0

    Now we have to keep track of where the good number line ends.

    for that when we traverse we can simply check if arr[i]!=0 then 
    goodNumber++;

    that way we can have the line end.


    Here tricky part is to swap, then a non zero is found we have to swap
    it to the end of goodNumber line

    

Code : 

```java
public static int[] moveZeros(int[] arr){
    int pos = 0;
    for(int i = 0 ; i < arr.length ; i ++){
        if(arr[i]!=0){
            //swap
            int temp = arr[pos];
            arr[pos] = arr[i];
            arr[i] = temp;
            //incrementing goodNumber line pos
            pos++;
        }
    }
    return arr;
}
```

## Left rotate by D

>**Problem**
Left roatate the given array by D times


Example :

    Input : 10 20 30 40
            2
    Output : 30 40 10 20

    Input : 10 20 30 40
            3
    Output : 40 10 20 30

Solution :

    Bruteforce :
     We know how to roate array by 1 , so we call rotate by 1 Method D times.
    
    Approach 1 :

    We take first d elements in array , and then append at the end of the array 

    Example :
    10 20 30 40
    3

    we take first 3 elements and store them in arrray [10 20 30]
    now we shift elements by d starting from dth index
    
    [40] 20 30 40*

    40 shifted from * to []
    now we insert the stored values from [10 20 30]

    40 [10 20 30]

    Now array has been rotated D times
Code : 
```java
public static int[] leftRotateByD(int[] arr, int d){
    int[] temp = new int[d];
    for(int i =0 ;i < d ;i++){
        temp[i] = arr[i];
    }
    for(int i = d ; i < arr.length ;i++){
        arr[i-d] = arr[i];
    }
    for(int i = arr.length - d, j =0 ; i < arr.length ;i++,j++){
        arr[i] = temp[j];
    }
    return arr;
}
```

    Approach 2 :

    There is another way without using the extra space, 
    
    if we look closely the ith elementh is always put at a calculated position

    for example :

    [40] 10 20 30
    d = 2

    res Array :

    20 30 [40] 10

    here 0th element 40 is placed at 2nd pos

    1st indexed ele 10 is at 3rd pos

    there is a relation between them

Code :

```java
public static int[] leftRotateAdvanced(int[] arr,int d){
    int nextPos = 0;
    for(int i = 0 ; i < arr.length ;i++){
        if(i-d < 0){
            nextPos = arr.length - (i-d);
        }
        else{
            nextPos = i -d ;
        }
        arr[nextPos] = arr[i];
    }
    return arr;
}
```


## Find the leaders 

>**Problem**
Given an array find the leader elements in that array ,

Leader element :
is an element which do not have any element greater than it to its right side.


Example :

    Input :  10 20 5 30 2
    Output : 2 30 

    5 is not leader as 30 is greater than it to its right side
    20 is also not leader as 30 is to its right
    similarly for 10

Solution :
[Link to solution](https://ide.geeksforgeeks.org/kZNeol7GKJ)

    Approach 1 :
    We traverse array from last to first .
    we set a max = arr[arr.length-1];

    now theory here is , at every point in iteration we always have a 
    max with us 

    and if next element is greater than currMax we change the max to new 
    and print that element.

    as we are traversing from back , we have one less problem to deal 
    with i.e to know if there is a bigger element to the right
    
    which is a problem when we are traversing from right


Code : 
```java
public static ArrayList<Integer> getLeaders(int[] arr){
ArrayList<Integer> aList = new ArrayList<Integer>();
int max = arr[arr.length-1];
aList.add(max);
    for(int i = arr.length-2 ; i >= 0 ; i--){
        if(max < arr[i]){
            max = arr[i];
            aList.add(arr[i]);
        }
    }
    return aList;
}
```

## Maximum difference in array

>**Problem**
Given an array find the maximum difference between arr[j] - arr[i]
and j > i
i.e J is always at the right of array.


Example :

	Input : 2 3 10 9 1 
	Output : 8

    As 2 - 10 pair give max diff

    1- 10 is invalid 

    Input : 30 10 8 2
    Output : -2

    the pair 10 - 8 gives maximun difference 

Solution :
[Link to solution]( https://ide.geeksforgeeks.org/eKkmrh9wSh)


    Here if we find the minimum element , then we can find the max 
    difference in O(n)
    then , we would only need to traverse through array and find the max 
    difference

    Approach :

    We assume the min element to be first Ele
    then we check for elements later to that till last
    if we get an element smaller than minEle we update the min ele
    if we get difference greater than current we update diff

Code : 
```java
public static int maxDiffAdv(int[] arr){
    int min = arr[0];
    int diff = Integer.MIN_VALUE;
    
    for(int i = 1 ; i < arr.length ; i++){
        diff = Math.max(diff,arr[i]-min);
        min = Math.min(min,arr[i]);
    }
    return diff;
}
```

## Stock buy and sell Problem

>**Problem**
Given N days stock values , we have to make maximum profit by buying and
selling .

Example :

	Input : 1 5 3 8 12
	Output : 13

    we buy at 1 and sell at 5 ,
    we again buy at 3 and sell at 12

    so 5-1 + 12- 3 = 4 + 9 = 13

Solution :
[Link to solution](https://ide.geeksforgeeks.org/2DwByHrLiX)


    Approach  :

    Here simple idea is to add only when next value is greater than current,

    if the next is smaller i.e we are declining we do not need to add that in profit

    also in the end we need to return the max profit.


    so from a point if we check for greater and add the values we will 
    get to a peak selling point and profit simultanously 


    example :
    1 5 7 3 8 12

    if we start checking from arr[i] we will reach till 7 
    and till that point we will add the diff as profit 

    so that will in turn give us profit from start to 7

    1 5 7  = > max profit => 6

    iteration wise 

    profit += arr[i+1]-arr[i] 

    and when array starts to get lower values we simply ignore till we 
    get a bigger value

Code : 
```java
public static int stockBS(int[] arr){
    int maxProfit = 0;

    for(int i = 1 ; i < arr.length ;i++){
        if(arr[i] > arr[i-1]){
            maxProfit+= arr[i] - arr[i-1];
        }
    }
    return maxProfit;
}
```

## Trapping water problem

>**Problem**
Given array of heights find the amount of water the structure can
trap

Example : 

	Input : 2 0 2
	Output : 2

    2 [] []
    1 [] []

    Here 2 0 2 is represented and the gap between 2 towers can hold 2 amount of water.

    Input : 3 0 1 2 5
    Output : 6

              []  
              [] 
    []        [] 
    []     [] [] 
    []  [] [] []


    if we take a look at the structure it can hold 6 amount of water

Solution :
[Link to solution](https://ide.geeksforgeeks.org/rKR6wcZcdF)

    The 0th and nth index cannot hold any water    
    Here main idea is knowing the maximum heights from left and right,

    at any point if we know maximum heights from left and right we know the amount of 
    water it can hold

    now to get this we precompute the left max and  right max for every index    

    left max :
        we create an empty array for leftMax[n]         
        we take arr[0] as left max 

        we iterate from 0 to n

        leftMax[i] = Math.max(arr[i],leftMax);
        so for  
        
        3 0 1 2 5

        we get 

        3 3 3 3 5

        and similarly right max

        5 5 5 5 5

        now we only need to find the minHeight between left and 
        right and subtract arr[i]    

Code : 
```java
public static int trapWater(int[] arr){
    int waterCap = 0;
    int leftMax = 0;
    int rightMax = 0;

    int[] lArr = new int[arr.length];
    int[] rArr = new int[arr.length];

    for(int i = 0 ; i < arr.length ; i++){
        leftMax = Math.max(arr[i],leftMax);
        lArr[i] = leftMax;
    }
    for(int i = arr.length -1 ; i >=0 ; i--){
        rightMax = Math.max(arr[i],rightMax);
        rArr[i] = rightMax;
    }

    for(int i= 0 ; i < arr.length ; i++){
        waterCap += Math.min(lArr[i],rArr[i]) - arr[i];
    }
    return waterCap;
}
```


## Maximum consecutive 1s

>**Problem**
Given a boolean array find the length of maximum consecutive 1s

Example :

	Input : 0 1 0 1 1 1 0 1 1
	Output : 3

    0 1 0 [1 1 1] 0 1 1 so 3 is the length

    Input : 0 1 0 0 
	Output : 1

Solution :
[Link to solution](https://ide.geeksforgeeks.org/CB2KT9XypS)

    we travese the arrya if we get 1 we increment count and maxCount variable, 
    if we get zero we reset the count 

Code : 
```java
public static int maxOnes(int[] arr){
    int maxCount = 0;
    int count = 0;
    for(int i = 0 ; i < arr.length ; i++){
        if(arr[i]==1){
            count++;
            maxCount = Math.max(maxCount,count);
        }
        else{
            count=0;
        }
    }
return maxCount;
}
```

## Maximum sub array sum [Kadane's Algorithm]

>**Problem**
Given array , find the maximum sub array sum
sub array can be a single element or consecutive array elements

Example :

	Input : 2 3 -6 8 4 2
	Output : 14

    2 3 -6 [8 4 2]
    this sub array gives maximum sum
    
    Input : 2 3 -11 87
    Output : 87

    last element gives maximum subarray sum

Solution :
[Link to solution](https://ide.geeksforgeeks.org/bnZ8edIhQr)

    Bruteforce :
    Here brute force is to start form i and check for every element and 
    make a sum out of them

    and store it in finalSum if current sum is > finalSum

    repeat for every element till N


    Kadane's Algorithm:

    2 3 -6 8 4 2
    consider an array , we will get maximum sum at any point if all the 
    values from the left are giving maximum sum

    for example : 20 30 40
    in this maximum sum is 90

    while traversing the array we have to calculate maximum sum till that point 

    to decide wheather to keep it or discard it 

    for example :

    2 -3 8

    in this at arr[2] , left max sum is [2 -3]=>-1
    so if we keep -1 and add it to 8 we will get 
    -1 + 8 => 7 

    which is less than 8 

    so the choice here at arr[2] is to keep leftSum or to keep selfvalue,
    whichever is greater    

Code : 
```java

public static int maxSubArraySum(int[] arr){
    int maxSum = 0;
    int sum = 0 ;
    for(int i = 0 ; i < arr.length ; i++){
        sum = Math.max(arr[i],sum+arr[i]);
        maxSum = Math.max(maxSum,sum);
    }
    return maxSum;
}
```

## Longest Odd even sub array

>**Problem**
Given an array find the longest odd even paired subarray,

Example :

	Input : 2 3 4 8
	Output : 3

    Here [2 3 4] 8 is the longest oddEven paired subarray

    Input : 2 6 10 12
    Output : 1

    Here no odd even paired so we return 1

Solution :
[Link to solution](https://ide.geeksforgeeks.org/Sp7XlX1yZ8)

    Approach : 
    Best approach here is to extend concept of Kadane's algorithm,

    "if everything is going good keep doing , if not reset the values"
        - Simplified Kadane's Algo
            -By shreyas

    Here if we found adjacent element is not odd even paired we will 
    start new subArray counting from there

    How to find if adjacent element is odd even paired !?
        3 + 3 = 6 even
        3 + 4 = 7 odd
        4 + 7 = 11 odd

        so if arr[i] + arr[i+1] == odd
        then count++ 

Code : 
```java
public static int lengthOfEvenOdd(int[] arr){
    int maxLen = 1;
    int res = 1;
    for(int i = 1 ; i < arr.length ; i++){
        if((arr[i-1]+arr[i]) % 2 == 1){
            res++;
            maxLen = Math.max(res,maxLen);
        }else{
            res = 1;
        }
    }
    return maxLen;
}
```

## Maximum circular sub array sum

>**Problem**
Given an array find the maximum sum subarray ,including circular subarrays

Example :

	Input : 2 -5 7 3
	Output : 12

    [2] -5 [7 3]

    is the maximum sum subarray

Solution :
[Link to solution](https://ide.geeksforgeeks.org/h8wjdmXCTd)

    Bruteforce :

    Now we already know how to calculate subarray sum using Kadane's algorithm

    we will calculate this for all the indexes of array,
    Here to go back in array we use % operator with length
    

Code : 
```java
public static int maxCircularSum(int[] arr){
    int length = arr.length;
    int maxSum = 0 ;
    int sum = 0;
    
    for(int i = 0 ; i < length ; i++){
        sum = 0;
        for(int j = i,count=0 ; j < length && count < length ;j = (j + 1) % length,count++){
            sum = Math.max(arr[j] + sum , arr[j]);
        }
        maxSum = Math.max(maxSum,sum);
    }
    return maxSum;
}
```

    Approach 1: 
    Thre result can be calculated using 
    maximum(regularArraySum , circularArraySum)

    regularArraySum => can be calulated with Kadane's algorithm,
    circularArraySum =>

    circularArraySum 

    There is a pattern in circular Array sum 

    for example : 

    3 -2 5 = > [3 5]

    4 5] -3 -7 [2 1 8

    if we take a close look here we are removing minimum subarray sub to get maximum circular subarray sum.


    we can get mimimum subarray sum using Kadane's algorithm

    Consider an example ,

     1  2  3 -2  -3  4  5 => 10 [total sum of array] 

    Here we have to find the minimum subarray sum

    to find that we will invert the array

    -1 -2 -3  2   3 -4 -5 , this way we will use kadane's algo and get 
    the 5 , but the 5 is minimum sum so we add them again in original array


    here reason to add is to recover from the damage the minimum array 
    has done to total

    But there is a special case for all the array elements as -ve

    for example ,

    -5 -3 = > -8

    if we keep doing our regular stuff we invert the array and 5 3 results
    in sum as 8 and when we add -8 + 8 we get 0

    and for -5 -3 maximum circular subarray sum is -3 , but our ans is 0

    so there is a special condition to prevent this 

    if our regular sum subarray is < 0 
    then we return regular sum subarray value


Code :
```java
public static int maxSumSub(int[] arr){
    int maxSum = 0;
    int sum = 0;
    for(int i = 0 ; i < arr.length;i++){
        sum = Math.max(arr[i],( arr[i] + sum ));
        maxSum = Math.max(sum,maxSum);
    }
    return maxSum;
}
public static int maxCirCSubArray(int [] arr){
    int circMax = 0 ;
    int maxSum = maxSumSub(arr);
    if(maxSum < 0){
        return maxSum;
    }
    int arrSum = 0;
    for(int i = 0 ; i< arr.length ; i++){
        arrSum+= arr[i];
        arr[i] = -arr[i];
    }    
    
    circMax = arrSum + maxSumSub(arr);
    return Math.max(circMax,maxSum);
}
```

## Majority Element [Moore's Voting algorithm]

>**Problem**
Given an array find the index of majority element
majority element : element with occurence > (arr.length / 2)

Example :

	Input : 2 3 4 4 4
	Output : 2

    Input : 20 10 40 50 50 50
    Output : -1


Solution :
[Link to solution](https://ide.geeksforgeeks.org/GiGZlUePfF)

    Approach :
    Here we are using moore's algorithm to calculate a majority element 
    
    Main idea is that if in an array there is majority then a pair will 
    have 
    a pair with 2 same elements 
    or 
    a single element


    for example 

    4 6 6 4 6

    pairs are

    4 6 
    6 4
    6  - here is an extra element with majority

    3 3 4 4 4 8 8 8 8 8

    pair 
    3 3
    4 4
    4 8
    8 8
    8 8

    if we see that 3 has majority in first pair
    similarly 4 has in second 
    8 has twice 

    
Code : 
```java
public static int majority(int[] arr){
    int res = 0;
    int count = 1;
    for(int i = 1 ; i < arr.length ; i++){
        if(arr[i] == arr[res]){
            count++;
        }else{
            count--;
        }
        if(count == 0){
            res = i;
            count = 1;
        }
    }
    count = 0;
    for(int i = 0 ; i < arr.length ;i++){
        if(arr[i] == arr[res]){
            count++;
        }
    }
    if(count > arr.length / 2){
        return arr[res];
    }
    return -1;
}
```

## Minimum flips to make a binary array same 

>**Problem**
Given a binary array find and print the minimum steps required to make the array same.

Example :

	Input : 1,1,0,0,1,0
	Output : 
        from 2 to 4
        from 5 to 5


Solution :
[Link to solution](https://ide.geeksforgeeks.org/FKwu2LcxRe)

    there are 2 ways to make the array same 
    either flip all 1s to make 0 OR
    flip all 0s to make 1

    now we just have to find out the minimum of them

    2nd group is always the minimum 

    for examaple :

    if we start our array with 1

    1 0 
    then 2nd group will be either 0 or no group
    1 1
    here there is no group 

    similarly 

    1,1,0,0,1

    here 2nd group is the minimum way
    
Code : 
```java
public static void minFlips(int[] arr){
    for(int i = 1 ; i < arr.length ; i++){
        if(arr[i] != arr[i-1]){
            
            if(arr[i]!=arr[0]){
                System.out.print("from "+i);
            }else{
                System.out.print(" to "+i);
                System.out.println();
            }
            if(i==arr.length-1){
                System.out.println(" to "+i);   
            }
        }
    }
}
```

## Maximum sum of K consecutive elements [Sliding window]

>**Problem**
Given an array , find the maximum sum in given range K 

Example :

	Input : 20 5 10 15 30 K= 3
	Output : [10 + 15 + 30] = 55

Solution :

[Link to solution](https://ide.geeksforgeeks.org/BOupKnipIW)

    Bruteforce : run 2 loops one for elemet range and other for summing 
    till range , return max of those    

Code:
```java
public static int maxKsum(int[] arr,int k){
    int maxSum = 0;
    for(int i = 0 ; i <= arr.length - k ; i++){
        int sum = 0;
        for(int j = i ; j < i+3 ;j++){
            sum += arr[j];
        }
        maxSum = Math.max(maxSum,sum);
    }
    return maxSum;
}
```

    Approach [sliding window way]: 
    In non sliding window way we do repetative work by calculating sum for imaginary windows of size K

    In sliding window we use previous calculated sum and alter the sum to keep window size maintained

    In maxK sum problem 

    we will first calculate the sum of K window, 
    Now to maintain window we will add the next element to the sum and remove the previous element.

Code : 
```java
public static int maxSumSW(int[] arr, int k){
    int maxSum = 0;
    int sum = 0;
    for(int i = 0 ; i < k ;i++){
        maxSum+=arr[i];
    }
    sum = maxSum;
    for(int i =1;i<=arr.length -k;i++){
        
        sum = (sum - arr[i-1]) + arr[i+k-1];
        maxSum = Math.max(sum,maxSum);
        
    }
    return maxSum;
}
```