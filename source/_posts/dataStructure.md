---
title: Data Structure
date: 2026-07-08
tags:
hide: true
description: Data Structure and Algorithms
---
# Sorting Algorithms
## Bubble Sort
``` Java
public void bubblesort(int[] a) {
    for (int i = 0; i < a.length; i++) {
        boolean flag = false;
        for (int j = 0; j < a.length; j++)
        {
            if (a[j] > a[j + 1])
            {
                int temp = a[j];
                a[j] = a[j + 1];
                a[j + 1] = temp;
                flag = true;
            }
        }
        if (!flag)
            return;
    }
}
```
## Insertion Sort
``` Java
public void insertionsort(int[] a) {
    for (int i = 1; i < a.length; i++)
    {
        int key = a[i];
        int j;
        for (j = i - 1; j >= 0; j--)
        {
            if (a[j] <= key)	
                break;
            a[j+1] = a[j];
        }
        a[j+1] = key;
    }
}
```
## Selection Sort
``` Java
public void selectionsort(int[] a) {
    int min = 0;
    for (int i = 0; i < a.length; i++)
    {
        min = i;
        for (int j = i + 1; j < a.length; j++)
        {
            if (a[j] < a[min])
                min = j;
        }
        int temp = a[min];
        a[min] = a[i];
        a[i] = temp;		
    }
}
```
## Heap Sort
``` Java
private static void swap(int [] a, int x, int y) {
    int temp = a[x];
    a[x] = a[y];
    a[y] = temp;
}

/*
    * The element at index c bubbles up the heap.
    * 
    * Running time O( log n ), or more precisely, O( log size ).
    */
private static void up(int[] a, int c) {
    if (c == 0) return;
    int p = (c - 1) / 2;
    if (a[c] <= a[p]) return;
    swap(a, c, p);
    up(a, p);
}

/*
    * The element at index p bubbles down the heap.
    * Unlike up, we need to pass {@code size}.
    *  
    * @param p the current node under consideration
    * @param size the size of the current heap, from index 0 to index size - 1. 
    *
    * Running time O( log n ), or more precisely, O( log size ).
    */
private static void down(int[] a, int p, int size) {
    if (p * 2 + 2 > size) return;
    int larger = p * 2 + 1;
    if (larger + 1 < size && a[larger] < a[larger+1]) 
        larger++;
    if (a[p] >= a[larger]) return;
    swap(a, p, larger);
    down(a, larger, size);
}

/*
    * The heapsort algorithm has two phases.
    * 
    * First, include elements into the virtual heap one by one.
    * Second, remove the max from the virtual heap one by one.
    *  
    * Running time O( n log n ).
    */    
public static void heapsort(int[] a) {
    for (int i = 1; i < a.length; i++)
        up(a, i);
    for (int i = a.length - 1; i > 0; i--) {
        swap(a, 0, i);  // similar to removeMax.
        down(a, 0, i);
        // Uncomment the following line to see the progress.
        // System.out.println(Arrays.toString(a));
    } 
}
```
## Binary Sort
## Merge Sort
``` Java
public static void mergesort(int[] a) {
    mergesort(a, 0, a.length- 1);
}
public static void mergesort(int[] a, int low, int high) {
    if (high < 1 + low) return;
    int mid = low + (high - low) / 2;
    mergesort(a, low, mid);
    mergesort(a, mid+1, high);
    merge(a, low, mid, high);
}
```
## Quick Sort
# Binary Search
``` Java
public int binarySearch(int[] a, int key) {
    int high = a.length - 1;
    int low = 0;
    int mid = low + (high - low)/2;
    while(high >= low)
    {
        if (key < a[mid])
        {
            high = mid - 1;
            mid = low + (high - low)/2;
        }
        else if (key > a[mid])
        {
            low = mid + 1;
            mid = low + (high - low)/2;
        }
        else 
            return mid;
    }
    return -1;
}
```
# Recursive Binary Search
``` Java
public int RBinary(int[] a, int key, int high, int low)
{
    if (low > high)
        return -1;
    int mid = low + (high - low)/2;
    if (a[mid] == key)
        return mid;
    return key > a[mid]?RBinary(a, key, high, mid + 1):RBinary(a, key, mid - 1, low);
}
```
# Balanced Brackets
``` Java
public static boolean isBalanced(String str){
    // Return true if and only if 'str' 
    // 1) is non-empty,
    // 2) contains only the six characters, and
    // 3) is balanced.

    if (str.isEmpty())
    {
        return false;
    }
    int n = str.length();
    char[] chars = str.toCharArray();
    char[] array = new char[n];
    int p = 0;
    for (int i = 0; i < n; i++)
    {
        if (p == 0)
        {
            if ((chars[i] == '(') || (chars[i] == '[') || (chars[i] == '{'))
                array[p++] = chars[i];
            else return false;
        }
        else {
            if ((chars[i] == '(') || (chars[i] == '[') || (chars[i] == '{'))
                array[p++] = chars[i];
            else if ((chars[i] == ')' && array[p - 1] == '(')
                    || (chars[i] == ']' && array[p - 1] == '[')
                    || (chars[i] == '}' && array[p - 1] == '{')) {
                p--;
            }
            else return false;
        }
    }
    return p == 0;
}
```
# Divide and Conquer
``` java
public static int recursivePeak(int[] a) {
    return recursivePeak(a, 0, a.length - 1);
}
private static int recursivePeak(int[] a, int l, int h) {
    if(l > h) return -1;
    if(l == h) return l; // L, not 1.

    int m = l + (h - l + 1) / 2; // the same as m = (l + h + 1) / 2, but safer.
    if (a[m] < a[m-1]) return recursivePeak(a, l, m - 1);
    else return recursivePeak(a, m, h);
    /*        
        * The following use two comparisons to eliminate a[m] as well.
    int m = l + (h - l) / 2; // l + (h - l + 1) / 2 also works.
    if (m > 0 && a[m] < a[m-1]) return recursivePeak(a, l, m - 1);
    else if (m < a.length-1 && a[m] < a[m+1]) return recursivePeak(a, m + 1, h);
    else return m;
    */
}
```
``` Java
public static int recursiveMax(int[] a) {
    if (a.length == 0) return -1;
    return max(a, 0, a.length-1);
}
private static int max(int[] a, int low, int high) {
    if (low >= high) return low;
    int mid = low + (high - low) / 2; // mid = (low + high) / 2
    int left = max(a, low, mid); // ceiling of n/2
    int right = max(a, mid+1, high); // floor of n/2
    return (a[left] >= a[right])? left:right; 
}
```
``` Java
public static int[] naiveMaxmin(int[] a) {
    if (a.length == 0) return null;
    int[] ans = new int[2];
    if (a.length == 1) {ans[0] = ans[1] = 0; return ans;}
    if (a[0] > a[1]) {ans[0] = 0; ans[1]= 1;}
    else {ans[0]= 1; ans[1] = 0;}
    /*
        * the last two lines can be replaced by
        *     ans[0] = (a[0] > a[1])? 0:1; 
        *     ans[1] = 1 - ans[0]; 
        */
    for (int i = 2; i < a.length; i++) {
        if (a[i] > a[ans[0]]) ans[0] = i; 
        else if (a[i] < a[ans[1]]) ans[1] = i;            
    }
    return ans;
}
```
``` Java
    public static int[] rMaxmin(int[] a) {
	return maxmin(a, 0, a.length - 1);
    }
    private static int[] maxmin(int[] a, int low, int high) {
        if (low > high) return null;  // wrong input
        int ans[] = new int[2];
        if (high == low) {  // base case one
            ans[0] = ans[1] = high; 
            return ans;
        }
        // Now an range of two is a base case.
        // iF YOU PARTITION IT, YOU DON'T SAVE THE 0.5 n.
        if (high == low + 1) { // base case two
            ans[0] = (a[low] > a[high])? low:high; 
            ans[1] = low - ans[0] + high;
            return ans;
        }
        
        // in the rest high - low >= 2. Easy.
        int mid = low + (high - low) / 2;
        int[] a1 = maxmin(a, low, mid);
        int[] a2 = maxmin(a, mid + 1, high);
        ans[0] = (a[a1[0]] > a[a2[0]])?a1[0]:a2[0]; // larger with the larger
        ans[1] = (a[a1[1]] < a[a2[1]])?a1[1]:a2[1]; // smaller with the smaller
        return ans;
    }
```