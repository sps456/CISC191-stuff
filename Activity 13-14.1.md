## Activity 13-14.1: Database
1. Flowchart of my thought process:

<img width="177" height="613" alt="image" src="https://github.com/user-attachments/assets/a9cf5e08-c099-485e-9b47-7f38c4b3c13e" />

2. The implementation of the code was not that difficult, neither was setting up the database in MySQL, but I had great difficulty adding the SQL connector driver to my IDE since I use net beans instead of what was shown in the video. I finally was able to do it with the help of a tutorial in another language, geeks for geeks, and remembering to unzip the downloaded file.
3. Video Explaination of Code:
https://drive.google.com/file/d/1x635JDgG1QQIvi-TP-GWdmwfc9tQ2F3M/view?usp=sharing

4. Code:
SQL.java
``` java
import java.sql.*;
public class SQL {
  public static void main(String[] args)
      throws SQLException, ClassNotFoundException {
    // Load the JDBC driver
    Class.forName("com.mysql.cj.jdbc.Driver");
    System.out.println("Driver loaded");
    
    // Establish a connection
    // Assuming the database name is 'testdb', user is 'testuser'
    // and password is 'Pa$$word'
    Connection connection = DriverManager.getConnection
      ("jdbc:mysql://localhost/miramar","testuser","Pa$$word");
    System.out.println("Database connected");
    
    // Create a statement
    Statement statement = connection.createStatement();
    statement.execute("insert into Student (ssn,firstname,mi,lastname,birthDate,deptID)\n" +
"values ('111222333','Philip','D','Collins','1980-12-20','1234')\n" +
";");
    
    // Execute a statement
    ResultSet resultSet = statement.executeQuery
      ("select * from Student where ssn = '111222333';");
      
      // Iterate through the result and print the student names
    while (resultSet.next()){
      System.out.println(resultSet.getString(1) + "\t" +
        resultSet.getString(2) + "\t" + resultSet.getString(3) + "\t" +
        resultSet.getString(4) + "\t" + resultSet.getString(5) + "\t" + 
        resultSet.getString(6) + "\t" + resultSet.getString(7) + "\t" + 
        resultSet.getString(8) + "\t" + resultSet.getString(9));
    }
    statement.execute("update student set zipCode = '92126' where ssn = '111222333';");
    
    resultSet = statement.executeQuery
      ("select * from Student where ssn = '111222333';");
      
      // Iterate through the result and print the student names
    while (resultSet.next()){
      System.out.println(resultSet.getString(1) + "\t" +
        resultSet.getString(2) + "\t" + resultSet.getString(3) + "\t" +
        resultSet.getString(4) + "\t" + resultSet.getString(5) + "\t" + 
        resultSet.getString(6) + "\t" + resultSet.getString(7) + "\t" + 
        resultSet.getString(8) + "\t" + resultSet.getString(9));
    }
    
    statement.execute("delete from student where ssn = '111222333';");
    // Close the connection
    connection.close();
  }
}
```
