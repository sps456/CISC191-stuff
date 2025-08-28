## CISC 191 Assigment 1.1: Sorting
1. Thought Process Flowchart

![Assignment1_Flowchart](https://github.com/user-attachments/assets/637e729c-6ade-4464-bd7e-164e9d1896da)

2. I decided to use the bubble sort algorithm since it was suggested and the data set is guaranteed to be less than 20 integers, so the algorithm's inefficiencies likely won't be a factor.
3. Right out the gate I noticed that the assignment asked for the values to be in descending order, not ascending order as would be seen in a normal bubble sort, but that wasn't too difficult to work around since I could just loop through the array backwards. Other than that I didn't have too much trouble with the assignment (outside of a brief complication with displaying the final array using commas which I fixed by displaying it using spaces instead which allowed me to get rid of the weird looking comma at the end of the array).
4. Video Explanation of Code
https://drive.google.com/file/d/1uCbMJM4-aVgNZie-IxSJLQ176XRNi8Dv/view?usp=sharing
5. Final Code
```java
import java.util.Scanner;
public class Sorting {
    public static void main(String[] args) {
        int size;
        Scanner scan = new Scanner(System.in);
        size = scan.nextInt();
        int[] arr = new int[size];
        for(int i = 0; i < size; i++){
            arr[i] = scan.nextInt();
        }
        sortArray(arr,size);
        System.out.print("[ ");
        for(int i = 0; i < size; i++){
            System.out.print(arr[i] + " ");
        }
        System.out.print("]");
    }
    public static void sortArray(int[] myArr, int arrSize) {
        int temp = -1;
        for(int i = 0; i < arrSize; i++){
            for(int j = arrSize-1; j > 0; j--){
                if(myArr[j-1] < myArr[j]){
                    temp = myArr[j-1];
                    myArr[j-1] = myArr[j];
                    myArr[j] = temp;
                }
            }
        }
    }
}
```
