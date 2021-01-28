# Searching and sorting problems

## Binary Search [iterative]

>**Problem**
Given a sorted array and a Key . Return its position in an array.
if key doesnot exist in an array return -1.


Example :

	Input : 10 20 30 40 50 80 Key = 50
	Output : 4

    as 50 is on 4th index


Solution :
[Link to solution]()

    Binary Search is binary in nature i.e 0 OR 1 , true or false , left 
    or right

    so we are either looking at left or at right for a given position

    consider an example 

    10 20 30 40 50 80 Key = 50

    we know the array is sorted , so if we take a mid and compare Key 
    with it there are three possiblities

    1. Key is equal to mid
    2. Key > mid
    3. Key < mid

    if key is greater than mid i.e it exists in right of mid.

    so we ignore the left 

    similarly for Key < mid 

Code : 
```java
public static int binarySearch(int[] arr,int key){
    int low = 0 ; 
    int high = arr.length -1;
    
    int mid = (low + high) / 2;
    
    while(low <= high){
        mid = (low + high) /2 ;
        
        if(arr[mid] == key){
            return mid;
        }
        if(arr[mid] < key){
            low = mid + 1;
        }
        else{
            high = mid - 1;
        }
    }
    return -1;
}
```


## Binary Search [Recursive]

>**Problem**
Given a sorted array and a Key . Return its position in an array.
if key doesnot exist in an array return -1.


Example :

	Input : 10 20 30 40 50 80 Key = 50
	Output : 4

    as 50 is on 4th index


Solution :
[Link to solution]()

Code : 
```java
public static int binarySearchRec(int[] arr , int key , int start , int end){
    int mid = (start + end) / 2 ;
    if(start > end){
        return -1;
    }
    if(arr[mid] == key){
        return mid;
    }
    if(arr[mid] < key){
        return binarySearchRec(arr,key,mid+1,end);
    }else{
        return binarySearchRec(arr,key,start,mid-1);
    }
}
```

## First occurence of an element in an array

>**Problem**
Given a sorted array find the first occurence of the element 

Example :

	Input : 10 20 30 40 40 40 key = 40
	Output : 3

first occurence of 40 is at 3

Solution :
[Link to solution]()

    We use binary search to reduce the search items,

    if the element is greater than mid then we search on right half
    else left half

    if element is same as mid element 

    then there are 2 cases

    1 . is element first then we return the id 
    2. if element is not first then we check for left half for its first 
    occurences

Code : 
```java
public static int firstOccItr(int[] arr, int key,int start,int end){
    
    while(start <= end){
        int mid = (start + end) / 2;
        if(arr[mid] == key){
            if(mid == 0 || arr[mid-1]!=key){
                return mid;
            }
            else{
                end = mid-1;
            }
        }
        if(arr[mid] > key){
            end = mid-1;
        }
        if(arr[mid] < key){
            start = mid +1;
        }
    }
    return -1;
}
```

## Find the last occurence 

>**Problem**
Given a sorted array find the last occurence of Key

Example :

	Input : 10 20 40 40 40
	Output : 4

last occurence of 40 is at 4th index

Solution :
[Link to solution]()

    logic is same as of first occurence 

Code : 
```java
public static int lastOccItr(int[] arr, int key){
    int start = 0;
    int end = arr.length-1;
    
    while(start <= end){
        int mid = (start + end) / 2;
        
        if(arr[mid] > key){
            end = mid -1;
        }
        if(arr[mid] < key){
            start = mid +1;
        }
        if(arr[mid]==key){
            if(mid == arr.length-1 || arr[mid+1]!=key){
                return mid;
            }
            else{
                start = mid + 1;
            }
        }
    }
    return -1;
}
```


## Count Occurrences of K

>**Problem**
In Given sorted array count the occurences of element 

Example :

	Input : 10 20 40 40 40  Key = 40
	Output : 3

Here key = 40 comes 3 times

Solution :
[Link to solution]()

    As the array is sorted , if we count the first occurence of element
    and last occurence of element then we get a range of existence
    from that we can count the number of times it appears.

Code : 
```java
public static int occurencesOfK(int[] arr , int k){
    int firstOcc = firstOcc(arr,k);
    int lastOcc = lastOcc(arr,k);

    if(firstOcc == -1){
        return 0;
    }
    else{
        return (lastOcc - firstOcc) + 1;
    }
}
```


## Find the occurences of 1 Binaray Array

>**Problem**
Given a sorted binary array find the occurences of 1 

Example :

	Input : 0 0 0 0 1 1 1
	Output : 3

here 3 1s are there
    

Solution :
[Link to solution]()

    Simple way is to find the first occurence of 1 and find the range 
    using Length of array

Code : 
```java
public static int numOf1s(int[] arr){
    int firstOcc = firstOcc(arr, 1);

    if(firstOcc == -1){
        return 0;
    }
    else{
        return arr.length - firstOcc;
    }
}
```

## Square root

>**Problem**
Given a number find its square root in integer

Example :

	Input : 36
	Output : 6

	Input : 35
	Output : 5


Solution :
[Link to solution](https://ide.geeksforgeeks.org/vWEa0qvNdb)

    Bruteforce : Bruteforce way is to iterate from 1 
    till the product is < than number
    
Code : 
```java
public static int squareRoot(int x ){
    int res = 0;
    
    while(res * res <= x){
        res++;
    }
    return res-1;
}    
```

    Approach : 
    Another way to implement this is to use binary search 

    Now that we have number range in sorted 
    i.e from 
    1 to N

    we will simply divide and find the result 


Code :
```java
public static int squareRootEff(int x){
    int start = 1 ; 
    int end = x ;
    int mid = 0;
    while(start <= end){
        mid = (start + end) / 2;
        int tempSq = mid * mid;
        if(tempSq == x){
            return mid;
        }
        if(tempSq < x){
            start = mid + 1;
        }else{
            end = mid - 1; 
        }
    }
    return mid;
}
```    

## Search in Infinite sorted array

>**Problem**
Given an infinite sorted array , find the position of element

Example :

	Input : 10 20 30 40 50 ... K = 30
	Output : 2


Solution :
[Link to solution]()

    Bruteforce : 
    Bruteforce way is to do linear search and print 

    Efficient method : 
    we jump from ranges in powers of 2 ,
    
    if we get current element higher than the K then we make a binary 
    search from previous position to current position


Code : 
```java
public static int findInInfinite(int[] arr,int K){
    if(arr[0] == K){
        return 0;
    }
    int index = 1;
    
    while(arr[index] < K){
        if(arr[index] == K){
            return index;
        }
        index = index * 2;
    }
    return binarySearch(arr,index/2+1,index,K);
}
```

## Find position of element in sorted rotated array

>**Problem**
Given an sorted rotated array , find the postion of element 

Example :

	Input : 90 100 10 20 30   K = 10
	Output : 2


Solution :
[Link to solution]()

    Bruteforce : 
    Bruteforce way is to use linear search 

    Efficient Approach :

        Sorted rotated array is sorted always in either left or right 
        from the mid point 

        Example :

        4 5 6 7 8 9 = > Original 
        8 9 4 5 6 7 = > Rotated twice

        8 9 [4] [5 6 7]

        Now ,

        We just have to find in which part we are looking 
        based on Sorted part and Range,
        After we have found the range we again do the same steps
        we will make array half every time getting 
        log(N) complexity


Code : 
```java
public static int searchInRotated(int[] arr , int k){
    int start = 0 ;
    int end = arr.length-1;
    
    int mid = 0;
    
    while(start <= end ){
        mid = ( start + end ) / 2 ;
        
        if(arr[mid] == k){
            return mid;
        }
        if(arr[mid] <= arr[end]){
            if( k >= arr[mid] && k <= arr[end]){
                start = mid +1;
            }
            else{
                end = mid -1;
            }
        }
        else {
            if( k >= arr[start] && k <= arr[mid]){
                end = mid -1;
            }
            else{
                start = mid +1;
            }
        }
    }
    return -1;
}
```

## Find peak Element

>**Problem**
Given an unsorted array , return the peak element

Peak element : element which has both neighbours lower than self.

Example :

	Input : 5 10 20 30 7
	Output : 30

    As 20 < 30 > 7 


Solution :
[Link to solution](https://ide.geeksforgeeks.org/yNYC2Z7CTt)


    bruteforce : 
        Bruteforce way is to find the highest element and return it
    
    Efficient Approach:
        In any given array there is always a peak element

        for example :

        10 20 => 20
        20 20 => 20
        40 = > 40
        10 20 30 => 30

        Also one thing to note here is peak is found in direction where
        Value of neighbour is higher

        10 20 30 = > 30 [right side]
        30 20 10 = > 30 [left side]
        10 30 20 = > 30 [mid]

        4 5 30 10 = > 30 [right to mid]        mid = 1 ;


        So we divide array based on this fact 

        if element is found at mid return mid 

        if not check for which array to choose 
        repeat the steps 

        Tip : OR operation makes life easy by skipping next half if first 
        is true.

Code : 
```java
public static int findPeak(int[] arr){
    int start = 0 ; 
    int end = arr.length-1;
    int len = arr.length;
    
    while(start <= end){
        int mid = (start + end ) / 2;
        
        if((mid==len-1 || mid == 0) || (arr[mid] >= arr[mid +1] && arr[mid] >= arr[mid-1])){
            return arr[mid];
        }
        if(arr[mid-1]>arr[mid]){
            end = mid-1;   
        }
        else{
            start = mid +1;
        }
    }
    return -1;
}
```

## find pair for given sum [two pointer approach]

>**Problem**
Given a sorted array find a pair which has sum equal to given SUM

Example :

	Input : 10  5 17 20 40 sum = 22
 	Output : Yes

     There exist a pair for 22 => 5 + 17


Solution :
[Link to solution](https://ide.geeksforgeeks.org/30981SspdV)

    Two pointer approach :

    In sorted array the given sum will exist with 2 conditions

    1. One of them is smaller than other
    2. Both are equal

    Now considering we can use the fact that one of them is smaller and we have sorted array

    We can do some optimizations


    Here we are using 2 pointers to keep track of sum

Code : 
```java
public static boolean pairExists(int[] arr,int sum){
    int start = 0 ;
    int end = arr.length-1;
    
    while(start < end){
        int temp = arr[start] + arr[end];
        if(temp == sum){
            return true;
        }
        if(temp > sum){
            end=end-1;
        }
        else{
            start = start +1;
        }
    }
    return false;
}
```

## Find triplet sum [two pointer]

>**Problem**
Given a sorted array find 
if there exists a triplet which has sum equal to given sum

Example :

	Input : 5 10 20 30 15 sum = 40
	Output : true 

    There exists a triplet 

    5 + 20 + 15 => 40

Solution :
[Link to solution](https://ide.geeksforgeeks.org/dZdvRjkmkr)


    Bruteforce :
    Bruterforce way is to use 3 loops and do the magic

    Efficient Apprach :

    We already know how to calculate pair in O(n)

    so for every element till last length - 2 we will call for pairExist() function


Code : 
```java
public static boolean tripletExists(int[] arr, int sum){
    for(int i = 0 ; i < arr.length-2;i++){
        if(pairExists(arr,i+1,arr.length-1,sum-arr[i])){
            return true;
        }
    }
    return false;
}
```

##  Median of 2 sorted array

>**Problem**
Given 2 sorted array find the median of them

Example :

	Input : 2 4 5 9 | 7 8 10 40
	Output :

    As combined array will be 
    2 4 5 7 8 9 10 40
    The length is 8 which is even so we take 7 + 8 / 2 => 7.5

    If the combined array is of odd length then middle element is the 
    median

Solution :
[Link to solution](https://www.youtube.com/watch?v=yD7wV8SyPrc)

    Bruteforce approach :
    Bruteforce approach is to create a new Array
    and add all the elements and sort them

    After sorting calculate the median

    Efficient Appraoch :

        if we make a partition between the complete array
        For the left part :
        We can say that there will be some elements from first array and 
        some from second array

        same can be said for the right part 

        Example :

        Arr 1 : 1 5 8 10 18 20
        Arr 2 : 2 3 6 7

        Combined : 1 2 3 5 6 | 7 8 10 18 20

        The | indicates median or mid partition

        



Code : 
```java
```