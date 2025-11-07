## Assignment 10-11.1: GUI
1. Flowchart of my thought process:

<img width="201" height="520" alt="image" src="https://github.com/user-attachments/assets/fdd240e9-5e48-46d8-932d-2dd17a55e3a7" />

2. This was easily out most complex reading and code implimentation yet, but by closely paying attention to the reading examples, I was able to write this program largely without issue. You just gotta keep track of all of the different imports, their implimentations, and their final positions within the JFrame.
3. Video Explaination of Code:
https://drive.google.com/file/d/1ofKEHZ975ArfLb4NKQ06wYyAp1XA-M7E/view?usp=sharing

4. Code:

SalaryGUI.java
``` java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import java.awt.event.ActionEvent;
import java.awt.event.ActionListener;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JTextField;
public class SalaryGUI extends JFrame implements ActionListener {
    private JLabel wageLabel;
    private JLabel hourLabel;
    private JLabel salaryLabel;
    private JTextField wageField;
    private JTextField hourField;
    private JTextField salaryField;
    
    SalaryGUI(){
        setTitle("Salary Calculator");
        GridBagConstraints layoutConstraint = null;
        wageLabel = new JLabel("Enter Hourly Wage: ");
        hourLabel = new JLabel("Enter Hours Worked per Week: ");
        salaryLabel = new JLabel("Calculated Salary: ");
        
        wageField = new JTextField(15);
        wageField.setEditable(true);
        wageField.addActionListener(this);
        hourField = new JTextField(15);
        hourField.setEditable(true);
        hourField.addActionListener(this);
        salaryField = new JTextField(15);
        salaryField.setEditable(false);
        
        setLayout(new GridBagLayout());
        layoutConstraint = new GridBagConstraints();
        layoutConstraint.gridx = 0;
        layoutConstraint.gridy = 0;
        layoutConstraint.insets = new Insets(10,10,10,10);
        add(wageLabel,layoutConstraint);
        
        layoutConstraint = new GridBagConstraints();
        layoutConstraint.gridx = 1;
        layoutConstraint.gridy = 0;
        layoutConstraint.insets = new Insets(10,10,10,10);
        add(wageField,layoutConstraint);
        
        layoutConstraint = new GridBagConstraints();
        layoutConstraint.gridx = 0;
        layoutConstraint.gridy = 1;
        layoutConstraint.insets = new Insets(10,10,10,10);
        add(hourLabel,layoutConstraint);
        
        layoutConstraint = new GridBagConstraints();
        layoutConstraint.gridx = 1;
        layoutConstraint.gridy = 1;
        layoutConstraint.insets = new Insets(10,10,10,10);
        add(hourField,layoutConstraint);
        
        layoutConstraint = new GridBagConstraints();
        layoutConstraint.gridx = 0;
        layoutConstraint.gridy = 2;
        layoutConstraint.insets = new Insets(10,10,10,10);
        add(salaryLabel,layoutConstraint);
        
        layoutConstraint = new GridBagConstraints();
        layoutConstraint.gridx = 1;
        layoutConstraint.gridy = 2;
        layoutConstraint.insets = new Insets(10,10,10,10);
        add(salaryField,layoutConstraint);
    }
    
    @Override 
    public void actionPerformed(ActionEvent event){
        String wageInput = wageField.getText();
        double wage = Double.parseDouble(wageInput);
        String hourInput = hourField.getText();
        int hours = Integer.parseInt(hourInput);
        
        salaryField.setText(Double.toString(wage * hours * 52));     
    }
    public static void main(String[] args){
        SalaryGUI myGUI = new SalaryGUI();
        myGUI.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        myGUI.pack();
        myGUI.setVisible(true);
    }
}
```
