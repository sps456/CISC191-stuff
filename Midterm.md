## Version 1.0: The InventoryItem parent class and its 3 subclasses

InventoryItem.java
``` java
public class InventoryItem {
    protected String companyName;
    protected String itemName;
    public InventoryItem(String company,String item){
        companyName = company;
        itemName = item;
    }
    public void setComapanyName(String comp){
        companyName = comp;
    }
    public void setItemName(String item){
        itemName = item;
    }
    public void displayItem(){
        System.out.println("Company Name: " + companyName + "\nItem Name: " + itemName);
    }
}
```
 
Painkillers.java
``` java
public class Painkillers extends InventoryItem {
    protected String expirationDate;
    protected String ageGroup;
    public Painkillers(String companyName, String itemName, String expire, String ageGroup){
        super(companyName, itemName);
        expirationDate = expire;
        this.ageGroup = ageGroup;
    }
    public Painkillers(String companyName, String itemName, String expire){       //<----- (Overloaded constructor)
        super(companyName, itemName);
        expirationDate = expire;
        ageGroup = "Ages 10+";
    }
    public void setExpirationDate(String exp){
        expirationDate = exp;
    }
    public void setAgeGroup(String age){
        ageGroup = age;
    }
    @Override                                            //<------- (Overrided method)
    public void displayItem(){
        super.displayItem();
        System.out.println("Expiration Date: " + expirationDate + "\nAge Group: " + ageGroup);
    }
}
```
 
Bandages.java
``` java
public class Bandages extends Painkillers{
    private boolean waterProof;
    public Bandages(String companyName, String itemName, String expirationDate, String ageGroup, boolean waterProof){
        super(companyName, itemName, expirationDate, ageGroup);
        this.waterProof = waterProof;
    }
    public void setWaterProofStatus(boolean wp){
        waterProof = wp;
    }
    @Override
    public void displayItem(){
        super.displayItem();
        if(this.waterProof){
            System.out.println("This bandage is waterproof");
        }
        else{
            System.out.println("This bandage is not waterproof");
        }
    }
}
```
 
Equipment.java
``` java
public class Equipment extends InventoryItem{
    public double weight;
    public Equipment(String companyName, String itemName, double w){
        super(companyName, itemName);
        weight = w;
    }
    public void setWeight(double w){
        weight = w;
    }
    @Override
    public void displayItem(){
        super.displayItem();
        System.out.println("Weight: " + weight);
    }
}
```

## Version 2.0: A test class which will try a program and catch any InputMismatchException's or ArrayIndexOutOfBoundsException's

MidtermTest.java
``` java
import java.util.Scanner;
import java.util.InputMismatchException;
public class MidtermTest {
   public static void main(String[] args) {
       try{
       Scanner scan = new Scanner(System.in);
       InventoryItem a = new InventoryItem("Company","Item");
       Painkillers b = new Painkillers("Pharma", "Tylenol", "October 13th");
       Bandages c = new Bandages("Band Aid", "Standard", "October 18th", "Ages 3+", scan.nextBoolean());
       Equipment d = new Equipment("Equipment Maker", "MRI Machine", scan.nextDouble());
       InventoryItem[] shelf = new InventoryItem[4];
       shelf[0] = a;
       shelf[1] = b;
       shelf[2] = c;
       shelf[3] = d;
       System.out.println("Which item would you like to display?");
       int index = scan.nextInt();
       shelf[index].displayItem();
       scan.close();
       }
       catch(InputMismatchException excpt){
           System.out.println("ERROR: You have entered an invalid value");
       }
       catch(ArrayIndexOutOfBoundsException excpt){
           System.out.println("ERROR: You have entered an invalid shelf index");
       }
       
   }
}
```

## Version 3.0: Creates a user defined exception InvalidWeightException, updates Equipment.java to throw it if weight < 0, and catches this exception in the main test class

InvalidWeightException.java
``` java
public class InvalidWeightException extends Exception {
    public InvalidWeightException(){
        super("ERROR: You have entered an invalid weight");
    }
}
```

updated Equipment.java
``` java
public class Equipment extends InventoryItem{
    public double weight;
    public Equipment(String companyName, String itemName, double w) throws InvalidWeightException{
        super(companyName, itemName);
        if(w<0){
            throw new InvalidWeightException();      //<---- added this exception throw
        }
        else{
            weight = w;
        }
    }
    public void setWeight(double w)throws InvalidWeightException{
        if(w<0){
            throw new InvalidWeightException();      //<---- added this exception throw
        }
        else{
        weight = w;
        }
    }
    @Override
    public void displayItem(){
        super.displayItem();
        System.out.println("Weight: " + weight);
    }
}
```

updates MidtermTest.java
``` java
import java.util.Scanner;
import java.util.InputMismatchException;
public class MidtermTest {
   public static void main(String[] args) {
       try{
       Scanner scan = new Scanner(System.in);
       InventoryItem a = new InventoryItem("Company","Item");
       Painkillers b = new Painkillers("Pharma", "Tylenol", "October 13th");
       Bandages c = new Bandages("Band Aid", "Standard", "October 18th", "Ages 3+", scan.nextBoolean());
       Equipment d = new Equipment("Equipment Maker", "MRI Machine", scan.nextDouble());
       InventoryItem[] shelf = new InventoryItem[4];
       shelf[0] = a;
       shelf[1] = b;
       shelf[2] = c;
       shelf[3] = d;
       System.out.println("Which item would you like to display?");
       int index = scan.nextInt();
       shelf[index].displayItem();
       scan.close();
       }
       catch(InputMismatchException excpt){
           System.out.println("ERROR: You have entered an invalid value");
       }
       catch(ArrayIndexOutOfBoundsException excpt){
           System.out.println("ERROR: You have entered an invalid shelf index");
       }
       catch(InvalidWeightException excpt){     //<---- added this exception catch for InvalidWeightException
           System.out.println(excpt.getMessage());
       }
       
   }
}
```
