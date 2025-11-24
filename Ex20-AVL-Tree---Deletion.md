# Ex20 Sorting an Array using Merge Sort Algorithm
## DATE: 01-11-25
## AIM:
To design a program that sorts a given array of integers in ascending order without using built-in sorting functions, achieving O(n log n) time complexity and minimal space usage.
## Algorithm
1. Start the program.
2. Divide the array into two halves using recursion
3. Continue dividing until each subarray contains a single element.
4. Merge the subarrays in sorted order using a helper merge function.
5. Return the fully sorted array.
6. Display the sorted array.
   

## Program:
```
/*
Program to sort a given array of integers in ascending order without using built-in sorting functions
Developed by: SHAKTHI KUMAR S
RegisterNumber: 212222110043
*/
import java.util.*;

public class MergeSort {
    public static void merge(int arr[], int left, int mid, int right) {
        int n1 = mid - left + 1;
        int n2 = right - mid;

        int L[] = new int[n1];
        int R[] = new int[n2];

        for (int i = 0; i < n1; ++i)
            L[i] = arr[left + i];
        for (int j = 0; j < n2; ++j)
            R[j] = arr[mid + 1 + j];

        int i = 0, j = 0, k = left;
        while (i < n1 && j < n2) {
            if (L[i] <= R[j])
                arr[k++] = L[i++];
            else
                arr[k++] = R[j++];
        }
        while (i < n1)
            arr[k++] = L[i++];
        while (j < n2)
            arr[k++] = R[j++];
    }

    public static void sort(int arr[], int left, int right) {
        if (left < right) {
            int mid = (left + right) / 2;
            sort(arr, left, mid);
            sort(arr, mid + 1, right);
            merge(arr, left, mid, right);
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter number of elements: ");
        int n = sc.nextInt();
        int arr[] = new int[n];
        System.out.println("Enter the elements:");
        for (int i = 0; i < n; i++)
            arr[i] = sc.nextInt();
        sort(arr, 0, n - 1);
        System.out.println("Sorted array: " + Arrays.toString(arr));
        sc.close();
    }
}
```

## Output:
<img width="620" height="297" alt="514902221-5fc90908-90ae-4e4d-9ab6-e2c41a45e87a" src="https://github.com/user-attachments/assets/f6483e9e-fa69-4a22-bce1-fb0d7c423b4d" />



## Result:
The program has been successfully implemented and executed.
It sorts the given array of integers in ascending order using the Merge Sort algorithm with a time complexity of O(n log n) and minimal extra space.
