## CISC 191: Java Intermediates Final Project
1. Code

AutoFill.java
```java
import java.sql.*;
import java.util.Scanner;
import java.io.FileInputStream;
import java.io.IOException;
public class AutoFill {
    public static void main(String[] args) throws IOException, SQLException, ClassNotFoundException {
        //FIRST INPUT FILE INFORMATION INTO AUTOMPG SQL
        FileInputStream carStream = new FileInputStream("Auto.txt");
        Scanner scan = new Scanner(carStream);
        Class.forName("com.mysql.cj.jdbc.Driver");
        Connection connection = DriverManager.getConnection
        ("jdbc:mysql://localhost/Auto","testuser","Pa$$word");
        System.out.println("Database connected");
        Statement statement = connection.createStatement();
        while(scan.hasNextLine()){
            String line = scan.nextLine();
            String[] values = line.split("\\t");
            String mpg = "'" + values[0] + "'";
            String cylinders = "'" + values[1] + "'";
            String disp = "'" + values[2] + "'";
            String hp = "'" + values[3] + "'";
            String weight = "'" + values[4] + "'";
            String accel = "'" + values[5] + "'";
            String year = "'" + values[6] + "'";
            String origin = "'" + values[7] + "'";
            String name = "'" + values [8] + "'";
            if(mpg.equals("'NA'")){
                statement.execute("insert into AutoMPG (cylinders,displacement,horsepower,weight,"
                   + "acceleration,year,origin,name)\n"
                   + "values (" + cylinders + "," + disp + "," + hp + "," + weight + "," + accel 
                   + "," + year + "," + origin + "," + name + ")\n");
            }
            else if(hp.equals("'NA'")){
                statement.execute("insert into AutoMPG (mpg,cylinders,displacement,weight,"
                   + "acceleration,year,origin,name)\n"
                   + "values (" + mpg + "," + cylinders + "," + disp + "," + weight + "," + accel 
                   + "," + year + "," + origin + "," + name + ")\n");
            }
            else{
                statement.execute("insert into AutoMPG (mpg,cylinders,displacement,horsepower,weight,"
                   + "acceleration,year,origin,name)\n"
                   + "values (" + mpg + "," + cylinders + "," + disp + "," + hp + "," + weight + "," + accel 
                   + "," + year + "," + origin + "," + name + ")\n");
            }
        }
    }
}
```

TextGUI.java
``` java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JButton;
import javax.swing.JTextField;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JScrollPane;
import javax.swing.JTextArea;
import javax.swing.JSlider;
import java.sql.*;
import java.io.IOException;
public class TextGUI extends JFrame implements ActionListener{
    private JTextArea outputArea;
    private JButton searchButton;
    private JTextField inputField;
    private JLabel inputLabel;
    private JLabel outputLabel;
    private JLabel hpLabel;
    private JLabel mpgLabel;
    private JSlider hpSlider;
    private JSlider mpgSlider;
    private Connection connection;
    TextGUI() throws IOException, ClassNotFoundException, SQLException{
        GridBagConstraints layoutConst = null;
        setTitle("Auto Database Search");
        inputLabel = new JLabel("Input:");
        outputLabel = new JLabel("Automobiles Found:");
        hpLabel = new JLabel("Horse Power");
        mpgLabel = new JLabel("MPG");
        inputField = new JTextField(15);
        inputField.setEditable(true);
        outputArea = new JTextArea(15,50);
        JScrollPane scroll = new JScrollPane(outputArea);
        outputArea.setEditable(false);
        searchButton = new JButton("Search");
        searchButton.addActionListener(this);
        hpSlider = new JSlider(0,150,75);
        hpSlider.setMajorTickSpacing(25);
        hpSlider.setMinorTickSpacing(5);
        hpSlider.setPaintTicks(true);
        hpSlider.setPaintLabels(true);
        mpgSlider = new JSlider(0,40,20);
        mpgSlider.setMajorTickSpacing(10);
        mpgSlider.setMinorTickSpacing(2);
        mpgSlider.setPaintTicks(true);
        mpgSlider.setPaintLabels(true);
        
        
        setLayout(new GridBagLayout());
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 5, 1);
        layoutConst.anchor = GridBagConstraints.LINE_START;
        layoutConst.gridx = 0;
        layoutConst.gridy = 0;
        add(inputLabel, layoutConst);
        
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 5, 1);
        layoutConst.gridx = 1;
        layoutConst.gridy = 0;
        add(inputField, layoutConst);
        
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 5, 1);
        layoutConst.gridx = 2;
        layoutConst.gridy = 0;
        add(searchButton, layoutConst);
        
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 5, 1);
        layoutConst.gridx = 0;
        layoutConst.gridy = 1;
        add(mpgLabel, layoutConst);
        
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 5, 1);
        layoutConst.gridx = 1;
        layoutConst.gridy = 1;
        add(hpLabel, layoutConst);
        
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 5, 1);
        layoutConst.gridx = 0;
        layoutConst.gridy = 2;
        add(mpgSlider, layoutConst);
        
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 5, 1);
        layoutConst.gridx = 1;
        layoutConst.gridy = 2;
        add(hpSlider, layoutConst);
        
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 5, 1);
        layoutConst.anchor = GridBagConstraints.LINE_START;
        layoutConst.gridx = 0;
        layoutConst.gridy = 3;
        add(outputLabel, layoutConst);
        
        layoutConst = new GridBagConstraints();
        layoutConst.insets = new Insets(10, 10, 5, 1);
        layoutConst.fill = GridBagConstraints.HORIZONTAL;
        layoutConst.gridx = 0;
        layoutConst.gridy = 4;
        layoutConst.gridwidth = 5;
        add(scroll, layoutConst);
        
        Class.forName("com.mysql.cj.jdbc.Driver");
        connection = DriverManager.getConnection
        ("jdbc:mysql://localhost/Auto","testuser","Pa$$word");
    }
    
    @Override
    public void actionPerformed(ActionEvent event){
        try{
        String search = inputField.getText();
        String mpg = "'" + mpgSlider.getValue();
        String hp = "'" + hpSlider.getValue();
        System.out.println("mpg: " + mpg + "\thp: " + hp);
        Statement statement = connection.createStatement();
        ResultSet resultSet;
        outputArea.setText("");
        if(search.equals("ALL")){
            resultSet = statement.executeQuery("select * from AutoMPG where mpg like " + mpg + "%' or horsepower like " + hp + "%';");
            while (resultSet.next()){
                outputArea.append(resultSet.getString(1) + "  " +
                resultSet.getString(2) + "  " + resultSet.getString(3) + "  " +
                resultSet.getString(4) + "  " + resultSet.getString(5) + "  " + 
                resultSet.getString(6) + "  " + resultSet.getString(7) + "  " + 
                resultSet.getString(8) + "\t" + resultSet.getString(9) + "\n");
        }
        }
        else{
            search = "\"" + search;
            resultSet = statement.executeQuery("select * from AutoMPG where name like '" + search + "%' and (mpg like " 
            + mpg + "%' or horsepower like " + hp + "%');");
            while (resultSet.next()){
                outputArea.append(resultSet.getString(1) + "  " +
                resultSet.getString(2) + "  " + resultSet.getString(3) + "  " +
                resultSet.getString(4) + "  " + resultSet.getString(5) + "  " + 
                resultSet.getString(6) + "  " + resultSet.getString(7) + "  " + 
                resultSet.getString(8) + "\t" + resultSet.getString(9) + "\n");
            }
        }
        }
        catch(Exception exepct){
            
        }
    }
    public static void main(String[] args) throws IOException, ClassNotFoundException, SQLException{
        TextGUI text = new TextGUI();
        text.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        text.pack();
        text.setVisible(true);
        
    }
}
```

2. Video Explaination of Code:
https://drive.google.com/file/d/1_0MrLYMU52nJ1yqDty6bUF79LzYLukH2/view?usp=sharing 
