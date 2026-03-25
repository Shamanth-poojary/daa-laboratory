# 📑 Index

- [Merge Sort Implementation](#merge-sort-implementation)
- [Quick Sort Implementation](#quick-sort-implementation)
- [Binary Search Tree (Insertion and Deletion)](#binary-search-tree-insertion-and-deletion)
- [Breadth-First Search (BFS) Implementation](#breadth-first-search-bfs-implementation)
- [Topological Sort (Using DFS)](#topological-sort-using-dfs)
- [Warshall's Algorithm (Transitive Closure)](#warshalls-algorithm-transitive-closure)
- [Heap Sort Implementation](#heap-sort-implementation)

---

---

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

# Breadth-First Search (BFS) Implementation

## 1. Code

```java
package daa_lab;
import java.util.*;

public class bfs {
public static void breadth(int[][] graph,int start,int vertices)
{
	boolean[] visited = new boolean[vertices];
	Queue<Integer> queue = new LinkedList<>();
	visited[start]=true;
	queue.add(start);
	while(!queue.isEmpty())
	{
		int current = queue.poll();
		System.out.print(current+" ");
		for(int i =0;i<vertices;i++)
		{
			if(graph[current][i]==1&&!visited[i])
			{
				visited[i]=true;
				queue.add(i);
			}
		}
	}
}
public static void main(String[] args) {
    Scanner sc = new Scanner(System.in);

    System.out.print("Enter number of vertices: ");
    int v = sc.nextInt();

    int[][] graph = new int[v][v];

    System.out.println("Enter adjacency matrix:");
    for (int i = 0; i < v; i++) {
        for (int j = 0; j < v; j++) {
            graph[i][j] = sc.nextInt();
        }
    }

    System.out.print("Enter starting vertex: ");
    int start = sc.nextInt();

    System.out.println("BFS Traversal:");
    breadth(graph, start, v);

    sc.close();
}
}
```

## 2. Algorithm

```text
Algorithm Breadth(graph, start, vertices)
    Create a boolean array 'visited' of size 'vertices' initialized to false
    Create an empty queue 'queue'

    Mark visited[start] = true
    Add 'start' to the queue

    While queue is not empty
        Remove the front node from the queue and assign it to 'current'
        Print 'current'

        For i = 0 to vertices - 1
            If there is an edge from 'current' to 'i' (graph[current][i] == 1) AND 'i' is not visited
                Mark visited[i] = true
                Add 'i' to the queue
        End For
    End While
END Breadth
```

## 3. Sample Output

```text
Enter number of vertices: 4
Enter adjacency matrix:
0 1 1 0
1 0 0 1
1 0 0 1
0 1 1 0
Enter starting vertex: 0
BFS Traversal:
0 1 2 3
```

# Topological Sort (Using DFS)

## 1. Code

```java
package daa_lab;
import java.util.*;

public class topo {
    int vertices;
    List<Integer>[] adj;

    topo(int v) {
        vertices = v;
        adj = new LinkedList[vertices];

        for (int i = 0; i < vertices; i++) {
            adj[i] = new LinkedList<>();
        }
    }

    void addEdge(int v, int w) {
        adj[v].add(w);
    }

    void dfs(int v, boolean[] visited, Stack<Integer> stack) {
        visited[v] = true;

        for (int n : adj[v]) {
            if (!visited[n]) {
                dfs(n, visited, stack);
            }
        }

        stack.push(v);
    }

    void topoSort() {
        Stack<Integer> stack = new Stack<>();
        boolean[] visited = new boolean[vertices];

        for (int i = 0; i < vertices; i++) {
            if (!visited[i]) {
                dfs(i, visited, stack);
            }
        }


        System.out.println("Topological Sort:");
        while (!stack.isEmpty()) {
            System.out.print(stack.pop() + " ");
        }
    }

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Enter the number of vertices: ");
        int V = scanner.nextInt();

        topo g = new topo(V);

        System.out.println("Enter the adjacency matrix:");
        for (int i = 0; i < V; i++) {
            for (int j = 0; j < V; j++) {
                if (scanner.nextInt() == 1) {
                    g.addEdge(i, j);
                }
            }
        }

        g.topoSort();
        scanner.close();
    }
}
```

## 2. Algorithm

```text
Algorithm dfs(v, visited, stack)
    Mark visited[v] = true
    For each neighbor 'n' of vertex 'v'
        If 'n' is not visited
            dfs(n, visited, stack)
        End If
    End For
    Push vertex 'v' onto the stack
END dfs

Algorithm topoSort()
    Create an empty Stack 'stack'
    Create a boolean array 'visited' of size 'vertices' initialized to false

    For i = 0 to vertices - 1
        If 'i' is not visited
            dfs(i, visited, stack)
        End If
    End For

    While stack is not empty
        Pop a vertex from the stack and print it
    End While
END topoSort
```

## 3. Sample Output

```text
Enter the number of vertices: 4
Enter the adjacency matrix:
0 1 1 0
0 0 0 1
0 0 0 1
0 0 0 0
Topological Sort:
0 2 1 3
```

# Warshall's Algorithm (Transitive Closure)

## 1. Code

```java
package daa_lab;
import java.util.*;

public class warshalls {
	public static void main(String[] args)
	{
		Scanner sc = new Scanner(System.in);
		System.out.println("enter the no of vertices");
		int n =sc.nextInt();
		int[][] graph =new int[n][n];
		System.out.println("enter the adjacency matrix");
		for(int i =0; i<n;i++)
		{
			for(int j =0; j<n;j++)
			{
				graph[i][j]=sc.nextInt();
			}
		}
		for(int k =0;k<n;k++)
		{
			for(int i =0;i<n;i++)
			{
				for(int j=0;j<n;j++)
				{
					graph[i][j]=graph[i][j]|graph[i][k]&graph[k][j];
				}
			}
		}
		 System.out.println("Transitive Closure:");
	        for (int i = 0; i < n; i++) {
	            for (int j = 0; j < n; j++) {
	                System.out.print(graph[i][j] + " ");
	            }
	            System.out.println();
	        }

	        sc.close();
	}

}
```

## 2. Algorithm

```text
Algorithm Warshalls()
    Read the number of vertices 'n'
    Create an 'n x n' adjacency matrix 'graph'
    Read the adjacency matrix elements from the user

    For k = 0 to n - 1
        For i = 0 to n - 1
            For j = 0 to n - 1
                Set graph[i][j] = graph[i][j] OR (graph[i][k] AND graph[k][j])
            End For
        End For
    End For

    Print the updated 'graph' matrix as the Transitive Closure
END Warshalls
```

## 3. Sample Output

```text
enter the no of vertices
4
enter the adjacency matrix
0 1 0 0
0 0 1 0
0 0 0 1
0 0 0 0
Transitive Closure:
0 1 1 1
0 0 1 1
0 0 0 1
0 0 0 0
```

# Heap Sort Implementation

## 1. Code

```java
package daa_lab;
import java.util.*;

public class heap {
	public static void main(String[] args)
	{
		Scanner sc = new Scanner(System.in);
		System.out.println("enter the number of elements in the array");
		int n =sc.nextInt();
		System.out.println("enter the array elements");
		int[] arr = new int[n];
		for (int i =0;i<n;i++)
		{
			arr[i]=sc.nextInt();
		}
		long startTime = System.nanoTime();
		heapsort(arr,n);
		long endTime = System.nanoTime();
		System.out.println("Sorted array: " + Arrays.toString(arr));
		long duration = endTime - startTime;
		System.out.println("Time taken for sorting: " + duration + " nanoseconds");
		sc.close();
	}
	public static void heapsort(int[] arr,int n)
	{
		for(int i =n/2-1;i>=0;i--)
		{
			heapify(arr,n,i);
		}
		for(int i=n-1;i>0;i--)
		{
			int temp =arr[0];
			arr[0]=arr[i];
			arr[i]=temp;
			heapify(arr,i,0);
		}
	}
	public static void heapify(int[] arr,int n,int i)
	{
		int largest =i;
		int left =2*i+1;
		int right = 2*i+2;
		if(left<n&&arr[left]>arr[largest])
		{
			largest=left;
		}
		if(right<n&&arr[right]>arr[largest])
		{
			largest=right;
		}
		if(largest!=i)
		{
			int swap =arr[i];
			arr[i]=arr[largest];
			arr[largest]=swap;
			heapify(arr,n,largest);
		}
	}

}
```

## 2. Algorithm

```text
Algorithm HeapSort(arr, n)

    *Phase 1: Build a max heap from the array
    For i from (n / 2) - 1 down to 0
        Call Heapify(arr, n, i)
    End For

    *Phase 2: Extract elements one by one from the heap
    For i from (n - 1) down to 1

        *Move current root (maximum element) to the end
        Swap arr[0] with arr[i]

        *Call max heapify on the reduced heap to restore heap property
        Call Heapify(arr, i, 0)

    End For

END HeapSort


Algorithm Heapify(arr, n, i)

    Initialize largest = i     //Assume the root is the largest
    Calculate leftChild = 2 * i + 1
    Calculate rightChild = 2 * i + 2

    *If left child exists and is greater than the root
    If leftChild < n AND arr[leftChild] > arr[largest]
        Set largest = leftChild
    End If

    *If right child exists and is greater than the largest so far
    If rightChild < n AND arr[rightChild] > arr[largest]
        Set largest = rightChild
    End If

    *If the largest is not the root, swap and continue heapifying
    If largest != i
        Swap arr[i] with arr[largest]

        *Recursively heapify the affected sub-tree
        Call Heapify(arr, n, largest)
    End If

END Heapify
```

## 3. Sample Output

```text
enter the number of elements in the array
6
enter the array elements
12 11 13 5 6 7
Sorted array: [5, 6, 7, 11, 12, 13]
Time taken for sorting: 145200 nanoseconds
```

# Horspool's String Matching Algorithm

## 1. Code

```java
package daa_lab;
import java.util.*;

public class horsepool {
public static void main(String[] args)
{
	Scanner sc = new Scanner(System.in);
	System.out.print("Enter the text: ");
	String text = sc.nextLine();
	System.out.print("Enter the pattern to search for: ");
	String pattern = sc.nextLine();
	long startTime = System.nanoTime();
	int index = search(text, pattern);
	long endTime = System.nanoTime();
	if (index != -1)
	{
	System.out.println("Pattern found at index: " + index);
	}
	else {
	System.out.println("Pattern not found.");
	}
	double timeElapsed = (endTime - startTime) / 1e6;
	System.out.println("total time taken:"+timeElapsed+"nanoseconds");
	sc.close();
}
public static int search(String text,String pattern)
{
	int[] table =shift(pattern);
	int n = text.length();
	int m =pattern.length();
	int i=m-1;
	while(i<n)
	{
		int k =0;
		while(k<m&&pattern.charAt(m-1-k)==text.charAt(i-k))
			k++;
		if(k==m)
			return i-m+1;
		i+=table[text.charAt(i)];
	}
	return -1;
}
public static int[] shift(String pattern)
{
	int m =pattern.length();
	int[] table = new int[256];
	for(int i =0;i<256;i++)
		table[i]=m;
	for(int i=0;i<m-1;i++)
		table[pattern.charAt(i)]=m-i-1;
	return table;
}
}
```

## 2. Algorithm

```text
Algorithm HorspoolSearch(text, pattern)

    * Pre-compute the shift table based on the pattern
    Set table = Call ShiftTable(pattern)
    Set n = length of text
    Set m = length of pattern

    * Align the right end of the pattern with the text
    Set i = m - 1

    While i < n
        Set k = 0

        * Compare pattern from right to left
        While k < m AND pattern[m - 1 - k] == text[i - k]
            Increment k
        End While

        * If the entire pattern matched
        If k == m
            Return (i - m + 1)     * Return the starting index of the match
        End If

        * Shift the pattern based on the bad-character heuristic
        Set i = i + table[text[i]]

    End While

    Return -1     * Pattern was not found in the text

END HorspoolSearch


Algorithm ShiftTable(pattern)

    Set m = length of pattern
    Create an array 'table' of size 256

    * Initialize all ASCII characters to the maximum shift (pattern length)
    For i from 0 to 255
        Set table[i] = m
    End For

    * Calculate actual shift values based on the characters in the pattern
    * (excluding the last character of the pattern)
    For i from 0 to m - 2
        Set table[pattern[i]] = m - i - 1
    End For

    Return table

END ShiftTable
```

## 3. Sample Output

```text
Enter the text: Hello World from Java
Enter the pattern to search for: World
Pattern found at index: 6
total time taken:0.1842nanoseconds
```

# 0/1 Knapsack Problem (Dynamic Programming)

## 1. Code

```java
package daa_lab;
import java.util.*;

public class knap {
	public static void main(String[] args)
	{
		Scanner sc = new Scanner(System.in);
		System.out.println("enter the number of items ");
		int n = sc.nextInt();
		int[] weights =new int[n];
		int[] values = new int[n];
		System.out.println("enter the weights ");
		  for (int i = 0; i < n; i++) {
	            weights[i] = sc.nextInt();
	        }

	        System.out.println("Enter the values of the items:");
	        for (int i = 0; i < n; i++) {
	            values[i] = sc.nextInt();
	        }
	        System.out.print("Enter the knapsack capacity: ");
	        int capacity = sc.nextInt();

	        System.out.println("Dynamic Programming Matrix:");

	        int maxValue = knapsack(weights, values, capacity);

	        System.out.println("Maximum value: " + maxValue);

	        sc.close();
	}
	public static int knapsack(int[] weights,int[] values,int capacity)
	{
		int num =weights.length;
		int[][] dp = new int[num+1][capacity+1];
		for(int i =0;i<=num;i++)
		{
			for(int w =0;w<=capacity;w++)
			{
				if(i==0||w==0)
					dp[i][w]=0;
				else if(weights[i-1]<=w)
				{
					dp[i][w]=Math.max(values[i-1]+dp[i-1][w-weights[i-1]],dp[i-1][w]);
				}
				else
				{
					dp[i][w]=dp[i-1][w];
				}
			}
		}
		display(dp);
		return dp[num][capacity];
	}
	public static void display(int[][] dp)
	{
		for(int i=0;i<dp.length;i++)
		{
			for(int j=0;j<dp[i].length;j++)
			{
				System.out.print(dp[i][j]+" ");
			}
			System.out.println();
		}
	}

}
```

## 2. Algorithm

```text
Algorithm Knapsack(weights, values, capacity)

    Set num = length of weights array
    Create a 2D array 'dp' of size (num + 1) x (capacity + 1)

    * Build the DP table in a bottom-up manner
    For i from 0 to num
        For w from 0 to capacity

            * Base Case: 0 items or 0 capacity means 0 value
            If i == 0 OR w == 0
                Set dp[i][w] = 0

            * If the current item's weight is less than or equal to current capacity 'w'
            Else If weights[i - 1] <= w
                * Take the maximum of including the item OR excluding the item
                Set includedValue = values[i - 1] + dp[i - 1][w - weights[i - 1]]
                Set excludedValue = dp[i - 1][w]
                Set dp[i][w] = Max(includedValue, excludedValue)

            * If the current item's weight is strictly greater than current capacity 'w'
            Else
                * We cannot include this item, carry forward the previous maximum
                Set dp[i][w] = dp[i - 1][w]

            End If

        End For
    End For

    * Display the completed DP matrix
    Call Display(dp)

    * The bottom-right cell contains the maximum value possible
    Return dp[num][capacity]

END Knapsack


Algorithm Display(dp)

    For i from 0 to number of rows in dp
        For j from 0 to number of columns in dp
            Print dp[i][j] followed by a space
        End For
        Print a newline character
    End For

END Display
```

## 3. Sample Output

```text
enter the number of items
3
enter the weights
1 2 3
Enter the values of the items:
10 15 40
Enter the knapsack capacity: 5
Dynamic Programming Matrix:
0 0 0 0 0 0
0 10 10 10 10 10
0 10 15 25 25 25
0 10 15 40 50 55
Maximum value: 55
```

# Prim's Minimum Spanning Tree Algorithm

## 1. Code

```java
package daa_lab;

import java.util.Scanner;

public class prims {

    public static void main(String[] args) {

        int[][] w = new int[10][10];
        int[] sol = new int[10];

        int n, i, j, s, k = 0;
        int min, sum = 0;
        int u = 0, v = 0;
        int flag = 0;

        Scanner sc = new Scanner(System.in);

        System.out.println("Enter the number of vertices");
        n = sc.nextInt();

        for (i = 1; i <= n; i++)
            sol[i] = 0;

        System.out.println("Enter the weighted graph");
        for (i = 1; i <= n; i++) {
            for (j = 1; j <= n; j++) {
                w[i][j] = sc.nextInt();
            }
        }

        System.out.println("Enter the source vertex");
        s = sc.nextInt();

        sol[s] = 1;
        k = 1;

        while (k <= n - 1) {

            min = 99;
            u = 0;
            v = 0;

            for (i = 1; i <= n; i++) {
                for (j = 1; j <= n; j++) {

                    if (sol[i] == 1 && sol[j] == 0) {
                        if (w[i][j] < min) {
                            min = w[i][j];
                            u = i;
                            v = j;
                        }
                    }
                }
            }

            if (min == 99)
                break;

            sol[v] = 1;
            sum = sum + min;
            k++;

            System.out.println(u + "->" + v + "=" + min);
        }

        for (i = 1; i <= n; i++) {
            if (sol[i] == 0)
                flag = 1;
        }

        if (flag == 1)
            System.out.println("No spanning tree");
        else
            System.out.println("The cost of minimum spanning tree is " + sum);

        sc.close();
    }
}
```

## 2. Algorithm

```text
Algorithm PrimsMST()

    Read the number of vertices 'n', the adjacency matrix 'w', and source vertex 's'
    Create an array 'sol' and initialize all vertices as unvisited (0)

    * Mark the source vertex as visited
    Set sol[s] = 1
    Set sum = 0

    * A minimum spanning tree has exactly (n - 1) edges
    For k from 1 to n - 1
        Set min = infinity (represented as 99)
        Set u = 0, v = 0

        * Find the smallest edge connecting a visited vertex 'i' to an unvisited vertex 'j'
        For every visited vertex 'i' and every unvisited vertex 'j'
            If w[i][j] < min
                Set min = w[i][j]
                Set u = i
                Set v = j
            End If
        End For

        * If no valid edge is found, the graph is disconnected
        If min == infinity
            Break
        End If

        * Mark the destination vertex as visited and add to total cost
        Set sol[v] = 1
        Set sum = sum + min

        Print the added edge (u -> v) and its cost

    End For

    * If any vertex remains unvisited, a full spanning tree isn't possible
    If any vertex in 'sol' is still 0
        Print "No spanning tree"
    Else
        Print "The cost of minimum spanning tree is " + sum
    End If

END PrimsMST
```

## 3. Sample Output

```text
Enter the number of vertices
4
Enter the weighted graph
99 2 99 6
2 99 3 8
99 3 99 5
6 8 5 99
Enter the source vertex
1
1->2=2
2->3=3
3->4=5
The cost of minimum spanning tree is 10
```
