## Assignment 10-11.2: Distance GUI
1. Flowchart of my though process:

<img width="175" height="517" alt="image" src="https://github.com/user-attachments/assets/c362f1cb-a330-4572-85f5-a5d2eaaccb32" />

2. This assignment was largely similar to the last one, except I used a formatted text field this time. Due to their different constructors however, my first test had the miles field be incomprehensibly skinny since I forgot to set its columns to 15.
3. Video Code Explaination:
https://drive.google.com/file/d/1CLpcG-tpCULE2xRKG-0Rt3Pjjbol4t8Q/view?usp=sharing

 4. Code:
DistanceGUI.java
``` java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import java.text.NumberFormat;
import javax.swing.JButton;
import javax.swing.JFormattedTextField;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JOptionPane;
import javax.swing.JTextField;
public class DistanceGUI extends JFrame implements ActionListener {
    public JLabel mileLabel;
    public JLabel kmLabel;
    public JLabel mLabel;
    public JLabel feetLabel;
    public JFormattedTextField mileField;
    public JTextField kmField;
    public JTextField mField;
    public JTextField feetField;
    public JButton calc;
    DistanceGUI(){
        setTitle("Distance Converter");
        calc = new JButton("Calculate");
        calc.addActionListener(this);
        mileLabel = new JLabel("Enter Distance in Miles: ");
        kmLabel = new JLabel("Distance in Kilometers: ");
        mLabel = new JLabel("Distance in Meters ");
        feetLabel = new JLabel("Distance in Feet: ");
        
        kmField = new JTextField(15);
        kmField.setEditable(false);
        mField = new JTextField(15);
        mField.setEditable(false);
        feetField = new JTextField(15);
        feetField.setEditable(false);
        
        mileField = new JFormattedTextField(NumberFormat.getNumberInstance());
        mileField.setEditable(true);
        mileField.setColumns(15);
        
        setLayout(new GridBagLayout());
        GridBagConstraints con = new GridBagConstraints();
        con.gridx = 0;
        con.gridy = 0;
        con.insets = new Insets(10,10,10,10);
        add(mileLabel,con);
        
        con = new GridBagConstraints();
        con.gridx = 1;
        con.gridy = 0;
        con.insets = new Insets(10,10,10,10);
        add(mileField,con);
        
        con = new GridBagConstraints();
        con.gridx = 2;
        con.gridy = 0;
        con.insets = new Insets(10,10,10,10);
        add(calc,con);
        
        con = new GridBagConstraints();
        con.gridx = 0;
        con.gridy = 1;
        con.insets = new Insets(10,10,10,10);
        add(kmLabel,con);
        
        con = new GridBagConstraints();
        con.gridx = 1;
        con.gridy = 1;
        con.insets = new Insets(10,10,10,10);
        add(kmField,con);
        
        con = new GridBagConstraints();
        con.gridx = 0;
        con.gridy = 2;
        con.insets = new Insets(10,10,10,10);
        add(mLabel,con);
        
        con = new GridBagConstraints();
        con.gridx = 1;
        con.gridy = 2;
        con.insets = new Insets(10,10,10,10);
        add(mField,con);
        
        con = new GridBagConstraints();
        con.gridx = 0;
        con.gridy = 3;
        con.insets = new Insets(10,10,10,10);
        add(feetLabel,con);
        
        con = new GridBagConstraints();
        con.gridx = 1;
        con.gridy = 3;
        con.insets = new Insets(10,10,10,10);
        add(feetField,con);
    }
    @Override
    public void actionPerformed(ActionEvent event){
        double miles = ((Number)mileField.getValue()).doubleValue();
        if(miles >= 0){
        kmField.setText(Double.toString(miles*1.609));
        mField.setText(Double.toString(miles*1609));
        feetField.setText(Double.toString(miles*5280));
        }
        else{
            JOptionPane.showMessageDialog(this, "Please enter a positive distance value");
        }
    }
    public static void main(String[] args){
        DistanceGUI dist = new DistanceGUI();
        dist.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        dist.pack();
        dist.setVisible(true);
    }
}
```
