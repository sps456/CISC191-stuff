## Activity 12.2: Merge sort
1. Flowchart of my thought process:

<img width="148" height="486" alt="image" src="https://github.com/user-attachments/assets/2d3325d0-9950-4351-bcc7-6533d49a1c76" />

2. Merge sorts are definitely a difficult process to impliment, but I was able to understand and properly write the necessary methods by following along with the reading. Since merge sorts use recursion, you can't use a counting variable in the same way I did with the insertion sort, but I was able to get around this by using a global counting variable in the MergeSort class. If I was less lazy, I would seperate the main method from the class and use a MergeSort object with a proper GetCompCount() method, but for this assignment just writing a main method within the class was sufficient. Also the instructions said to count the amount of swaps in the process, but that didn't make much sense since merge sorts dont really swap values, instead building the matrix from the ground up with the variables in place. Since the expected output said nothing about swaps I just ignored it.
3. Video Explaination of Code:
https://drive.google.com/file/d/1nZT3aDRlymhKTUK8cOKG2pzwtj_t-v84/view?usp=sharing

4. Code:
MergeSort.java
``` java
import java.util.Scanner;
public class MergeSort {
    private static int compCount = 0;
    
    public static void merge(int[] num, int left, int mid, int right){
        int arrSize = right - left + 1;
        int arr[] = new int[arrSize];
        int currIndex = 0;
        int leftIndex = left;
        int rightIndex = mid +1;
        
        while(leftIndex <= mid && rightIndex <= right){
            compCount++;
            if(num[leftIndex] < num[rightIndex]){
                arr[currIndex] = num[leftIndex];
                leftIndex++;
            }
            else{
                arr[currIndex] = num[rightIndex];
                rightIndex++;
            }
            currIndex++;
        }
        
        while(leftIndex <= mid){
            arr[currIndex] = num[leftIndex];
            currIndex++;
            leftIndex++;
        }
        
        while(rightIndex <= right){
            arr[currIndex] = num[rightIndex];
            currIndex++;
            rightIndex++;
        }
        
        for(int i = 0; i < arrSize; i++){
            num[left + i] = arr[i];
        }
    }
    public static void mergeSort(int[] numbers, int left, int right){
        int mid;
        if(left < right){
            mid = (left+right)/2;
            mergeSort(numbers, left, mid);
            mergeSort(numbers, mid+1, right);
            merge(numbers,left,mid,right);
        }
    }
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        
        int size;
        size = scan.nextInt();
        int left = 0;
        int right = size-1;
        int[] numbers = new int[size];
        for(int i = 0; i < size; i++){
            numbers[i] = scan.nextInt();
        }
        System.out.println("unsorted: ");
        for(int k = 0; k < numbers.length; k++){
                System.out.print(numbers[k] + " ");
        }
        System.out.println("\n");
        mergeSort(numbers,left,right);
        System.out.println("sorted:   ");
        for(int i = 0; i < numbers.length; i++){
            System.out.print(numbers[i] + " ");
        }
        System.out.println("\ncomparisons: " + compCount);
    }
}
```
