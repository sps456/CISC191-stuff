## Assignment 7.1: Exceptions
1. Flowchart of my thought process

![ExceptionsFlowchart](https://github.com/user-attachments/assets/39755b1d-3d43-4826-8ab5-20b44328c285)

2. I didn't have any real challenges with this assignment. I thought I might have to create a custom exception which would have been an extra step but the assignment specifically says to throw an Exception object and to catch any Exception object thrown by stepsToMiles, which I assume was to simplify the assignment.
3. Video Explaination of Code:
https://drive.google.com/file/d/1PBXJ3o_gQSOojLkWfZTfH4xvr0HN0Uqo/view?usp=sharing

4. Code:

Pedometer.java
``` java
import java.util.Scanner;
public class Pedometer {
    public static void main(String[] args){
        Scanner scan = new Scanner(System.in);
        int steps = scan.nextInt();
        try{
            double miles = stepsToMiles(steps);
            System.out.printf("%.2f", miles);
        }
        catch(Exception excpt){
            System.out.println(excpt.getMessage());
        }
    }
    public static double stepsToMiles(int numSteps)throws Exception{
        if(numSteps < 0){
            throw new Exception("Exception: Negative step count entered.");
        }
        return (double)numSteps / 2000.0;
        
    }    
}
```
