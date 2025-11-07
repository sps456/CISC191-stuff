## Assignment 10-11.3: Spinner GUI
1. Flowchart of my thought process:

<img width="167" height="508" alt="image" src="https://github.com/user-attachments/assets/a503d9a0-196e-4f83-be1a-fe4729782052" />

2. This was again quite similar to the other GUI assignments, which made it pretty simple to impliment. I had a slight issue involving casting an Integer to a double but I quickly resolved it once I found out what was causing it.
3. Video Explaination of Code:
https://drive.google.com/file/d/1sFjCmsWOVhLDDBQrg_yqHmrbwDjS_GGn/view?usp=sharing

 4. Code:
SpinnerGUI.java
``` java
import java.awt.GridBagConstraints;
import java.awt.GridBagLayout;
import java.awt.Insets;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JSpinner;
import javax.swing.JTextField;
import javax.swing.SpinnerNumberModel;
import javax.swing.event.ChangeEvent;
import javax.swing.event.ChangeListener;
public class SpinnerGUI extends JFrame implements ChangeListener{
    private JLabel mileLabel;
    private JLabel kmLabel;
    private JSpinner mileSpinner;
    private JTextField kmField;
    SpinnerGUI(){
        setTitle("Convert Miles to km");
        int initDist = 0;
        int minDist = 0;
        int maxDist = 15;
        int stepVal = 1;
        
        mileLabel = new JLabel("Enter Distance in Miles: ");
        kmLabel = new JLabel("Distance in Kilometers: ");
        SpinnerNumberModel model = new SpinnerNumberModel(initDist,minDist,maxDist,stepVal);
        mileSpinner = new JSpinner(model);
        mileSpinner.addChangeListener(this);
        
        kmField = new JTextField(15);
        kmField.setEditable(false);
        
        setLayout(new GridBagLayout());
        GridBagConstraints con = new GridBagConstraints();
        con.insets = new Insets(10,10,10,10);
        con.gridx = 0;
        con.gridy = 0;
        add(mileLabel,con);
        
        con = new GridBagConstraints();
        con.insets = new Insets(10,10,10,10);
        con.gridx = 1;
        con.gridy = 0;
        add(mileSpinner,con);
        
        con = new GridBagConstraints();
        con.insets = new Insets(10,10,10,10);
        con.gridx = 0;
        con.gridy = 1;
        add(kmLabel,con);
        
        con = new GridBagConstraints();
        con.insets = new Insets(10,10,10,10);
        con.gridx = 1;
        con.gridy = 1;
        add(kmField,con);
    }
    @Override
    public void stateChanged(ChangeEvent event){
        Integer miles = (Integer)mileSpinner.getValue();
        kmField.setText(Double.toString(miles*1.609));
    }
    public static void main(String[] args){
        SpinnerGUI spin = new SliderGUI();
        spin.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
        spin.pack();
        spin.setVisible(true);
    }
}
```
