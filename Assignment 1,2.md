## Assignment 1.2: Words Frequency
1. Thought Process Flowchart

![Assignment2_Flowchart](https://github.com/user-attachments/assets/1ca93c8f-7e05-4bdf-bfe0-f2ed809a6136)

2. The principle for doing a frequency analysis of a web page is largely the same as this assignment just on a larger scale. It would be a lot like what I did, just with hundreds/thousands of words in the array instead of <20 words. I could hypothetically just copy paste the entire text of a webpage into this program and it would be able to do a frequency analysis of the words, but it would be quite inefficient and probably take a while.
3. The frequency method itself was quite simple, though I imagine you could run into issues if you didn't know how to make the check case insensitive, but actually propogating the list array was more difficult since it was entirely based on a String and there was no set length to make the array. I got around this by looping through the String and counting the spaces, since as long as I dont enter any unnecessary spaces the word count is one higher than the space count. Once I got that down the rest of the main method wasn't too difficult to write.
4. Code Explaination Video
https://drive.google.com/file/d/1PopGvIQSZXV-nvFLqC05G0XaqZtBapXL/view?usp=sharing
5. Final Code
```java
import java.util.Scanner;
public class WordFrequency {
    public static void main(String[] args) {
        int spaceCount = 0;
        String list;
        Scanner scan = new Scanner(System.in);
        list = scan.nextLine();
        for(int i = 0; i < list.length(); i++){
            if(list.charAt(i) == ' ')
                spaceCount++;
        }
        String[] listArr = new String[spaceCount+1];
        for(int i = 0; i < spaceCount; i++){
            listArr[i] = list.substring(0,list.indexOf(" "));
            list = list.substring(list.indexOf(" ")+1);
        }
        listArr[listArr.length - 1] = list;
        for (String listArr1 : listArr) {
            System.out.println(listArr1 + " " + getWordFrequency(listArr, listArr.length, listArr1));
        }
    }

    public static int getWordFrequency(String[] wordsList, int listSize, String currWord){
        int count = 0;
        for(int i = 0; i < listSize; i++){
            if(wordsList[i].toUpperCase().equals(currWord.toUpperCase()))
                count++;
        }
        return count;
    }
}
```
