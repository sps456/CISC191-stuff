## Assignment 5-6.1: Inheritance
1. Flowchart of my thought process:

![inheritanceFlowchat](https://github.com/user-attachments/assets/ba9b3374-a6bd-4c37-a623-a31c88930a55)

2. I didn't have any issues with this assignment. It was a pretty simple application of the basics of Inheritance.
3. Video Explaination of Code:
https://drive.google.com/file/d/1wjYqJR9QnQ6AFZVzFYtDA6GBu7h-FKxc/view?usp=sharing
4. Code:

The Person and Student classes were provided without alteration so I will just post the main class here
StudentDerivationFromPerson.java
``` java
public class StudentDerivationFromPerson {
   public static void main(String[] args) {
      Student courseStudent = new Student();

      courseStudent.setName("Smith");
      courseStudent.setAge(20);
      courseStudent.setID(9999);
      courseStudent.printAll();
      System.out.print(", ID: " + courseStudent.getID());

   }
}
```
