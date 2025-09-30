## Overriding Methods
1. Flowchart of my thought process

![OverridedMethodFlowchart](https://github.com/user-attachments/assets/dc2d7464-18fd-4ca4-bd83-ead90b304835)

2. The implimentation was pretty simple again even though this assignment was slightly more complex. I was able to use very similar formatting to the last assignment so I wouldn't say I had any problems with this assignment.
3. Video Explaination of Code:
https://drive.google.com/file/d/1Y2WyMts498Cv3saf7VttgAdevdOIFsiP/view?usp=sharing
4. Code:

Book.java
``` java
public class Book {
    private String title;
    private String author;
    private String publisher;
    private String date;
    public void setTitle(String t){
        title = t;
    }
    public String getTitle(){
        return title;
    }
    public void setAuthor(String a){
        author = a;
    }
    public String getAuthor(){
        return author;
    }
    public void setPublisher(String p){
        publisher = p;
    }
    public String getPublihser(){
        return publisher;
    }
    public void setDate(String d){
        date = d;
    }
    public String getDate(){
        return date;
    }
    public void PrintInfo(){
        System.out.println("Book Information:\n   Book Title: " + title + "\n   Author: " + author + "\n   Publisher: " + publisher);
        System.out.println("   Publication Date: " + date);
    }
}
```
Encyclopedia.java
``` java
public class Encyclopedia extends Book {
    private String edition;
    private int numPages;
    public void setEdition(String ed){
        edition = ed;
    }
    public String getEdition(){
        return edition;
    }
    public void setNumPages(int p){
        numPages = p;
    }
    public int getNumPages(){
        return numPages;
    }
    @Override
    public void PrintInfo(){
        super.PrintInfo();
        System.out.println("   Edition: " + edition + "\n   Number of Pages: " + numPages);
    }
}
```
BookMain.java
``` java
import java.util.Scanner;
public class BookMain {
   public static void main(String[] args) {
       Book b = new Book();
       Encyclopedia e = new Encyclopedia();
       Scanner scan = new Scanner(System.in);
       b.setTitle(scan.nextLine());
       b.setAuthor(scan.nextLine());
       b.setPublisher(scan.nextLine());
       b.setDate(scan.nextLine());
       e.setTitle(scan.nextLine());
       e.setAuthor(scan.nextLine());
       e.setPublisher(scan.nextLine());
       e.setDate(scan.nextLine());
       e.setEdition(scan.nextLine());
       e.setNumPages(scan.nextInt());
       b.PrintInfo();
       e.PrintInfo();
   }
}
```
