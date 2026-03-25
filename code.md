# Merge Sort Implementation

## 1. Java Code

```java
package daa_lab;
import java.util.*;

public class merge_sort {
 public static void mergeDiv(int[] a,int low,int high)
 {
	 if(high-low<=1)
		 return;
	 int mid = low+(high-low)/2;
	 mergeDiv(a,low,mid);
	 mergeDiv(a,mid,high);
	 merge(a,low,mid,high);
 }
 public static void merge(int[] a,int low,int mid,int high)
 {
	 int[] temp = new int[high-low];
	 int i=low,j=mid,k=0;
	 while(i<mid&&j<high)
	 {
		 if (a[i]<a[j])
		 {
			 temp[k++]=a[i++];
		 }
		 else
		 {
			 temp[k++]=a[j++];
		 }
	 }
	 while(i<mid)
		 temp[k++]=a[i++];
	 while(j<high)
		 temp[k++]=a[j++];
	 for ( k=0;k<temp.length;k++)
	 {
		 a[low++]=temp[k];
	 }
 }
 public static void main(String[] args)
 {
	 Scanner sc = new Scanner(System.in);
	 System.out.println("enter the number of elements");
	 int n =sc.nextInt();
	 int[] arr = new int[n];
	 System.out.println("enter the array elements");
	 for(int i =0;i<n;i++)
	 {
		 arr[i]=sc.nextInt();
	 }
	 long start = System.nanoTime();
	 mergeDiv(arr,0,n);
	 long end = System.nanoTime();
	 System.out.println("the sorted array is:");
	 for(int x:arr)
		 System.out.print(x+" ");
	 System.out.println("\ntotal time taken for execution:"+(end-start)+"nano seconds");
	 sc.close();
 }
}
```

## 2. Algorithm

```text
MergeSort(arr, low, high)
If (high - low > 1)
    mid = low + (high - low) / 2
    MergeSort(arr, low, mid)
    MergeSort(arr, mid, high)
    Merge(arr, low, mid, high)
End If
END MergeSort

Merge(arr, low, mid, high)
Create temp array of size (high - low)
i = low, j = mid, k = 0

While i < mid and j < high
    If arr[i] < arr[j]
        temp[k] = arr[i]
        i++, k++
    Else
        temp[k] = arr[j]
        j++, k++
End While

Copy remaining elements from left subarray
Copy remaining elements from right subarray

Copy temp back to original array
END Merge
```

## 3. Sample Output

```text
enter the number of elements
6
enter the array elements
12 11 13 5 6 7

the sorted array is:
5 6 7 11 12 13
total time taken for execution:125600nano seconds
```

# Quick Sort Implementation

## 1. Code

```java
package daa_lab;
import java.util.*;

public class quick_sort {
	 public static int partition(int[] a, int low, int high) {
	        int pivot = a[low];
	        int i = low + 1;
	        int j = high;

	        while (true) {
	            while (i <= high && a[i] <= pivot)
	                i++;

	            while (a[j] > pivot)
	                j--;

	            if (i < j) {
	                int temp = a[i];
	                a[i] = a[j];
	                a[j] = temp;
	            } else {
	                int temp = a[low];
	                a[low] = a[j];
	                a[j] = temp;
	                return j;
	            }
	        }
	    }
	public static void quickSort(int[] a,int low,int high)
	{
		if(low<high) {
			int p =partition(a,low,high);
			quickSort(a,low,p-1);
			quickSort(a,p+1,high);
		}
	}
	public static void main(String[] args)
	{
		Scanner sc =new Scanner(System.in);
		System.out.println("enter the number of elements in the array");
		int n = sc.nextInt();
		System.out.println("enter the array elements");
		int[] arr = new int[n];
		 for (int i = 0; i < n; i++)
	            arr[i] = sc.nextInt();
		   long start = System.nanoTime();

	        quickSort(arr, 0, n - 1);

	        long end = System.nanoTime();

	        System.out.println("Sorted array:");
	        for (int x : arr)
	            System.out.print(x + " ");

	        System.out.println("\nTime taken: " + (end - start) + " ns");

	        sc.close();
	}
}
```

## 2. Algorithm

```text
Algorithm partition(a, low, high)
    Set pivot = a[low]
    Set i = low + 1
    Set j = high
    While True
        While i <= high AND a[i] <= pivot
            Increment i
        End While
        While a[j] > pivot
            Decrement j
        End While

        If i < j
            Swap a[i] and a[j]
        Else
            Swap a[low] (the pivot) and a[j]
            Return j
        End If
    End While
END partition

Algorithm quickSort(a, low, high)
    If low < high
        Set p = partition(a, low, high)
        quickSort(a, low, p - 1)
        quickSort(a, p + 1, high)
    End If
END quickSort
```

## 3. Sample Output

```text
enter the number of elements in the array
6
enter the array elements
12 11 13 5 6 7
Sorted array:
5 6 7 11 12 13
Time taken: 114300 ns
```
