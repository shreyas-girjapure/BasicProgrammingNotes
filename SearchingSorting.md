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