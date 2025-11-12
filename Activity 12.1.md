## Activity 12.1: Insertion Sort
1. Flowchart of my thought process:

<img width="150" height="483" alt="image" src="https://github.com/user-attachments/assets/a1a89316-c9ea-4eb0-81df-ff0ea01a5ba9" />

2. The actual insertion sort implementation was pretty easy since it was clearly outlined in the reading, but I had quite an annoying time counting the amount of comparisons in the process. I couldn't figure out how to properly count them while the array value comparison was part of the while loops condition, but I realized I could just add it as an if statement to get the same loop utility and accurately count the comparisons.
3. Video Explaination of Code:
 https://drive.google.com/file/d/1LetdpSVk2lAgu8LPb8KibQIKRk3kRGbo/view?usp=sharing

4. Code:
SortingAlgo.java
``` java
import java.util.Scanner;
public class SortingAlgo {
    public static void insertSort(int [] arr){
        int comp = 0;
        int swap = 0;
        int i;
        int j;
        int temp;
        for(i=1; i<arr.length; i++){
            j = i;
            while(j > 0){
                comp++;
                if(arr[j] < arr[j-1]){
                    temp = arr[j];
                    arr[j] = arr[j-1];
                    arr[j-1] = temp;
                    j--;
                    swap++;
                }
                else{
                    break;
                }
            }
            for(int k = 0; k < arr.length; k++){
                System.out.print(arr[k] + " ");
            }
            System.out.println("");
        }
        System.out.println("");
        System.out.println("comparisons: " + comp + "\nswaps: " + swap);
    }
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int size;
        size = scan.nextInt();
        int[] numbers = new int[size];
        for(int i = 0; i < size; i++){
            numbers[i] = scan.nextInt();
        }
        for(int k = 0; k < numbers.length; k++){
                System.out.print(numbers[k] + " ");
        }
        System.out.println("\n");
        insertSort(numbers);
    }
}
```
