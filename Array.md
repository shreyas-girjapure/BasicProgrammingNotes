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