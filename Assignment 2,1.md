## CISC 191 Assignment 2.1: Salary Calc
1. Though Process Flowchart

![flowchart2 1](https://github.com/user-attachments/assets/87ac13df-022a-4f1e-8976-be9767fb89e6)

2. The new methods were quite straight forward, so the only difficulty was familiarizing myself with the provided classes in order to properly create the setter/overloaded constructor.
3. Video Code Explaination:
https://drive.google.com/file/d/1ZRE8NQ2TiSdboDdsswGk2Tsg98PS2qpL/view?usp=sharing 

4. Full Code:

Task A TaxTableTools.java:
``` java
public class TaxTableTools {

    /**
     * This class searches the 'search' table with a search argument and returns
     * the corresponding value in the 'value' table. Variable 'nEntries' has the
     * number of entries in each table.
     */
    private int[] search = {0, 20000, 50000, 100000, Integer.MAX_VALUE};
    private double[] value = {0.0, 0.10, 0.20, 0.30, 0.40};
    private int nEntries;

    // *********************************************************************** 
    // Default constructor 
    public TaxTableTools() {
        nEntries = search.length;  // Set the length of the search table
    }

    // *********************************************************************** 
    // FIXME: Write a void setter method that sets new values for the private
    //        search and value tables. Name the method: setTables
    //        The method receives as parameters tables from which to load the 
    //        search and value tables.
    public void setTables(int[] s, double[] v){
        search = s;
        value = v;
    }
    // *********************************************************************** 
    // Method to get a value from one table based on a range in the other table
    public double getValue(int searchArgument) {
        double result;
        boolean keepLooking;
        int i;

        result = 0.0;
        keepLooking = true;
        i = 0;

        while ((i < nEntries) && keepLooking) {
            if (searchArgument <= search[i]) {
                result = value[i];
                keepLooking = false;
            } else {
                ++i;
            }
        }

        return result;
    }
}
```
Task A IncomeTaxMain.java:
``` java
import java.util.Scanner;

public class IncomeTaxMain {

    // Method to prompt for and input an integer
    public static int getInteger(Scanner input, String prompt) {
        int inputValue;

        System.out.println(prompt + ": ");
        inputValue = input.nextInt();

        return inputValue;
    } // 

    // *********************************************************************** 
    public static void main(String[] args) {
        final String PROMPT_SALARY = "\nEnter annual salary (-1 to exit)";
        Scanner scnr = new Scanner(System.in);
        int annualSalary;
        double taxRate;
        int taxToPay;
        int i;

        int[] salary = {0, 20000, 50000, 100000, Integer.MAX_VALUE};
        double[] taxTable = {0.0, 0.10, 0.20, 0.30, 0.40};

        // Access the related class
        TaxTableTools table = new TaxTableTools();

        // FIXME: Call a setter method in the TaxTableClass that supplies new 
        //        tables for the class to work with. The method should be called
        //        with: table.setTables(salary, taxTable);
        table.setTables(salary, taxTable);
        // Get the first annual salary to process
        annualSalary = getInteger(scnr, PROMPT_SALARY);

        while (annualSalary >= 0) {
            taxRate = table.getValue(annualSalary);
            taxToPay = (int) (annualSalary * taxRate);     // Truncate tax to an integer amount
            System.out.println("Annual Salary: " + annualSalary
                    + "\tTax rate: " + taxRate
                    + "\tTax to pay: " + taxToPay);

            // Get the next annual salary
            annualSalary = getInteger(scnr, PROMPT_SALARY);
        }
    }
}
```
Task B TaxTableTools.java:
``` java
import java.util.Scanner;

public class TaxTableToolsB {

    /**
     * This class searches the 'search' table with a search argument and returns
     * the corresponding value in the 'value' table. Variable 'nEntries' has the
     * number of entries in each table.
     */
    private int[] search = {0, 20000, 50000, 100000, Integer.MAX_VALUE};
    private double[] value = {0.0, 0.10, 0.20, 0.30, 0.40};
    private int nEntries;

    // *********************************************************************** 
    // Default constructor 
    public TaxTableToolsB() {
        nEntries = search.length;  // Set the length of the search table
    }

    // *********************************************************************** 
    // Overloaded constructor
    public TaxTableToolsB(int[] s, double[] v){
        nEntries = s.length;
        search = s;
        value = v;
    }
    // *********************************************************************** 
    // Method to prompt for and input an integer
    public int getInteger(Scanner input, String prompt) {
        int inputValue = 0;

        System.out.println(prompt + ": ");
        inputValue = input.nextInt();

        return inputValue;
    }

    // *********************************************************************** 
    // Method to get a value from one table based on a range in the other table
    public double getValue(int searchArgument) {
        double result;
        boolean keepLooking;
        int i;

        result = 0.0;
        keepLooking = true;
        i = 0;

        while ((i < nEntries) && keepLooking) {
            if (searchArgument <= search[i]) {
                result = value[i];
                keepLooking = false;
            } else {
                ++i;
            }
        }

        return result;
    }
}
```
Task B IncomeTaxMain.java:
``` java
import java.util.Scanner;

public class IncomeTaxMainB {

    public static void main(String[] args) {
        final String PROMPT_SALARY = "\nEnter annual salary (-1 to exit)";
        Scanner scnr = new Scanner(System.in);
        int annualSalary;
        double taxRate;
        int taxToPay;
        int i;

        // Tables to use in the exercise are the same as in the TaxTableTools class
        //int [] salaryRange = {   0,  20000, 50000, 100000,  Integer.MAX_VALUE };
        //double [] taxRates = { 0.0,   0.10,  0.20,   0.30,               0.40 };
        // 2(a) Modify the salary and tax tables in the main method to use 
        // different salary ranges and tax rates.
        int[] salaryRange = {0, 30000, 60000, Integer.MAX_VALUE};
        double[] taxRates = {0.0, 0.25, 0.35, 0.45};

        // Access the related class
        //TaxTableToolsB table = new TaxTableToolsB();
        // 2(b)Use the just-created overloaded constructor to initialize 
        // the salary and tax tables.
        TaxTableToolsB table = new TaxTableToolsB(salaryRange, taxRates);

        // Get the first annual salary to process
        annualSalary = table.getInteger(scnr, PROMPT_SALARY);

        while (annualSalary >= 0) {
            taxRate = table.getValue(annualSalary);
            taxToPay = (int) (annualSalary * taxRate);     // Truncate tax to an integer amount
            System.out.println("Annual Salary: " + annualSalary
                    + "\tTax rate: " + taxRate
                    + "\tTax to pay: " + taxToPay);

            // Get the next annual salary
            annualSalary = table.getInteger(scnr, PROMPT_SALARY);
        }
    }
}
```
