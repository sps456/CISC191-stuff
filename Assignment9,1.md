## Assignment 9.1: Collections
1. Flowchart of my thought process:

![collectionsFlowchart](https://github.com/user-attachments/assets/98dc0f70-8296-4231-b932-ff88e26492bb)

2. I didn't have any issue creating the method, but I wanted to use a do while loop to repeatedly ask for words and call palindrome() until the user decides to stop, but I decided it would be too much effort for something unnecessary to the assignment.
3. Video Explaination of Code:
https://drive.google.com/file/d/1TREpQD8jxjDFk20h6PjRNqx8a0UjuN9W/view?usp=sharing

4. Code:

Palindrome.java
``` java
import java.util.LinkedList;
import java.util.Deque;
import java.util.Scanner;
public class Palindrome {
    public static void Palindrome(String word){
        String lowerWord = word.toLowerCase();
        Deque<Character> letterList = new LinkedList<Character>();
        boolean isIt = true;
        for(int i = 0; i < lowerWord.length(); i++){
            letterList.addLast(lowerWord.charAt(i));
        }
        if(letterList.size() == 1){
            System.out.println("Yes, " + word + " is a palindrome.");
        }
        else{
            while(letterList.size() > 1){
                if(letterList.pollFirst()!= letterList.pollLast()){
                    System.out.println("No, \"" + word + "\" is not a palindrome.");
                    isIt = false;
                    break;
                }
            }
            if(isIt)
                System.out.println("Yes, " + word + " is a palindrome.");
        }
    }
    public static void main(String[] args ){
        Scanner scan = new Scanner(System.in);
        System.out.println("Please enter a word to check if its a palindrome:");
        String word = scan.nextLine();
        Palindrome(word);
        scan.close();
    }
}
```
