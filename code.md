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

# Binary Search Tree (Insertion and Deletion)

## 1. Code

```java
package daa_lab;
import java.util.*;

class binary_search {

    static class Node {
        int data;
        Node left, right;

        Node(int item) {
            data = item;
            left = right = null;
        }
    }

    Node root;

    Node insert(Node root, int data) {
        if (root == null) {
            return new Node(data);
        }
        if (data < root.data)
            root.left = insert(root.left, data);
        else if (data > root.data)
            root.right = insert(root.right, data);
        return root;
    }

    Node delete(Node root, int data) {
        if (root == null)
            return null;

        if (data < root.data)
            root.left = delete(root.left, data);
        else if (data > root.data)
            root.right = delete(root.right, data);
        else {
            // Case 1: No child
            if (root.left == null && root.right == null)
                return null;

            // Case 2: One child
            if (root.left == null)
                return root.right;
            if (root.right == null)
                return root.left;

            // Case 3: Two children
            int min = minval(root.right);
            root.data = min;
            root.right = delete(root.right, min);
        }
        return root;
    }

    int minval(Node root) {
        while (root.left != null)
            root = root.left;
        return root.data;
    }

    void inorder(Node root) {
        if (root != null) {
            inorder(root.left);
            System.out.print(root.data + " ");
            inorder(root.right);
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        binary_search tree = new binary_search();

        System.out.println("Enter number of elements:");
        int n = sc.nextInt();

        System.out.println("Enter elements:");
        for (int i = 0; i < n; i++) {
            int val = sc.nextInt();
            tree.root = tree.insert(tree.root, val);
        }

        System.out.println("Inorder traversal:");
        tree.inorder(tree.root);

        System.out.println("\nEnter number of elements to delete:");
        int d = sc.nextInt();

        for (int i = 0; i < d; i++) {
            System.out.println("Enter element to delete:");
            int del = sc.nextInt();
            tree.root = tree.delete(tree.root, del);

            System.out.println("Inorder after deletion:");
            tree.inorder(tree.root);
            System.out.println();
        }

        sc.close();
    }
}
```

## 2. Algorithm

```text
Algorithm Insert(root, data)
    If root is NULL
        Return new Node(data)
    If data < root.data
        root.left = Insert(root.left, data)
    Else If data > root.data
        root.right = Insert(root.right, data)
    Return root
END Insert

Algorithm Delete(root, data)
    If root is NULL, Return NULL

    If data < root.data
        root.left = Delete(root.left, data)
    Else If data > root.data
        root.right = Delete(root.right, data)
    Else (Node to be deleted is found)
        Case 1: No children (leaf node)
            If root.left is NULL AND root.right is NULL, Return NULL
        Case 2: One child
            If root.left is NULL, Return root.right
            If root.right is NULL, Return root.left
        Case 3: Two children
            Find minimum value in the right subtree (minval)
            Replace root.data with this minimum value
            root.right = Delete(root.right, minimum value)

    Return root
END Delete

Algorithm Inorder(root)
    If root is not NULL
        Inorder(root.left)
        Print root.data
        Inorder(root.right)
END Inorder
```

## 3. Sample Output

```text
Enter number of elements:
5
Enter elements:
50 30 70 20 40
Inorder traversal:
20 30 40 50 70
Enter number of elements to delete:
2
Enter element to delete:
20
Inorder after deletion:
30 40 50 70

Enter element to delete:
30
Inorder after deletion:
40 50 70
```
