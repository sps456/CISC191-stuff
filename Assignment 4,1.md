## Activity 4.1: Input and Output
1. Flowchart of my thought process:

![inputoutput_flowchart](https://github.com/user-attachments/assets/dc8a97f7-04d4-494e-b04b-35b7effe7004)

2. The code itself was quite easy to write, but ran into a couple errors. The first one was just that I forgot to throw IOException which was pretty easy to fix, but then I kept getting FileNotFound even tho I had the text document named "ParkPhotos.txt" in the CISC191 folder. Turns out since it had .txt in the name I just had to append .txt in the FileInputStream file name to be "ParkPhotos.txt.txt". This looked silly though so I just renamed the file itself to "ParkPhotos".
3. Video Explaination of Code:
https://drive.google.com/file/d/19VqZ8ajvAxYlV7ijEMpVGjCPIxv-IkfG/view?usp=sharing
4. Complete Code:
PhotoOrganizer.java
```java
import java.util.Scanner;
import java.io.FileInputStream;
import java.io.IOException;
public class PhotoOrganizer {
    public static void main(String[] args) throws IOException {
        FileInputStream photoStream = new FileInputStream("ParkPhotos.txt");
        Scanner scan = new Scanner(photoStream);
        while(scan.hasNextLine()){
            String s = scan.nextLine();
            s = s.substring(0,s.indexOf("photo.jpg")) + "info.txt";
            System.out.println(s);
        }
        scan.close();
        photoStream.close();
    }
}
```
