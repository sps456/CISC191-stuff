## Assignment 5-6.2: Derived Classes
1. Flowchart of my though process:

![DerivedClassesFlowchart](https://github.com/user-attachments/assets/2c4ee43f-b45c-405c-9556-ef89f9cb8c91)

2. This was another pretty simple assignment, so I only had slight trouble with formatting the output of the PrintInfo method and the printlns. I also didn't realize we were supposed to input the info via scanner initially so I had to slightly reformat my code to add a scanner.
3. Video Explaination of Code:
https://drive.google.com/file/d/15FHT4Y8jOSCLUvfN_Nji3r_C8z4wZPh4/view?usp=sharing
4. Code:

Course.java
``` java
public class Course {
    private String courseNum;
    private String courseName;
    public void setNum(String num){
        courseNum = num;
    }
    public String getNum(){
        return courseNum;
    }
    public void setName(String name){
        courseName = name;
    }
    public String getName(){
        return courseName;
    }
    public void PrintInfo(){
        System.out.println("Course Information:\n   Course Number: " + courseNum + "\n   Course Name: " + courseName);
    }
}
```
OfferedCourse.java
``` java
public class OfferedCourse extends Course {
    private String profName;
    private String location;
    private String time;
    public void setProfName(String name){
        profName = name;
    }
    public String getProfName(){
        return profName;
    }
    public void setLocation(String loc){
        location = loc;
    }
    public String getLocation(){
        return location;
    }
    public void setTime(String t){
        time = t;
    }
    public String getTime(){
        return time;
    }
}
```
CourseMain.java
``` java
import java.util.Scanner;
public class CourseMain {
   public static void main(String[] args) {
       Scanner scan = new Scanner(System.in);
       Course dsd = new Course();
       dsd.setNum(scan.nextLine());
       dsd.setName(scan.nextLine());
       OfferedCourse esd = new OfferedCourse();
       esd.setNum(scan.nextLine());
       esd.setName(scan.nextLine());
       esd.setProfName(scan.nextLine());
       esd.setLocation(scan.nextLine());
       esd.setTime(scan.nextLine());
       scan.close();
       dsd.PrintInfo();
       esd.PrintInfo();
       System.out.println("   Instructor Name: " + esd.getProfName());
       System.out.println("   Location: " + esd.getLocation());
       System.out.println("   Time: " + esd.getTime());
   }
}
```
