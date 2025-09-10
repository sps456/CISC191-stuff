## Assignment 3.1: Memory Management
1. Flowchart of my thought process:

![assignment3flow](https://github.com/user-attachments/assets/b00678bb-5d81-4a5d-8f6a-07d84fa3b436)

2. I think I ended up making the example class more complex than it needed to be, which made tracing the stack and heap memory allocations more annoying, but overall writing the class was very simple. I also had some difficulty understanding the difference between stack and heap storage, but I eventually wrapped my head around it.
3. Video Explaination of Code:

https://drive.google.com/file/d/1cwhZr-gzDnrvaOuC--XHi9wLSfgqrq9I/view?usp=sharing

4. Working Code and "Stack and Heap" diagram:

Enemy.java:
``` java
import java.util.Random;
public class Enemy {
    private int hp;
    private int dmg;
    private String name;
    private boolean isABoss;
    
    public Enemy(){
        name = "Slime";
        hp = 5;
        dmg = 1;
        isABoss = false;
    }
    
    public Enemy(int hp, int dmg, String name, boolean isABoss){
        this.hp = hp;
        this.dmg = dmg;
        this.name = name;
        this.isABoss = isABoss;
    }
    
    public void hit(int atk){
        Random rand = new Random();
        int crit = rand.nextInt(5) + 1;
        if(crit > 4){
            atk *= 1.5;
            System.out.println("CRITICAL HIT!!");
        }
        if(this.isABoss)
            atk *= .75;
        this.hp -= atk;       
    }
    
    public int getHp(){
        return this.hp;
    }
    
    public String getName(){
        return this.name;
    }
    
    public int getDmg(){
        return this.dmg;
    }
}
```
EnemyTest.java:
``` java
public class EnemyTest {
    public static void main(String [] args){
        Enemy boss = new Enemy(5, 2, "Slime Lord", true);
        int lazyHp = 2;
        int lazyDmg = 5;
        
        System.out.println("The air becomes thick with miasma...");

        System.out.println("You attack the " + boss.getName());
        boss.hit(lazyDmg);
        System.out.println("The " + boss.getName() + " has " + boss.getHp() + " health remaining!!\n");
        
        if(boss.getHp() <= 0)
            System.out.println("The boss has fallen!! YOU WIN!!!");
        else{
            System.out.println("The " + boss.getName() + " attacks!");
            lazyHp -= boss.getDmg();
            System.out.println("You have " + lazyHp + " health remaining!!\n");
            System.out.println("Your bones will be digested for decades to come... YOU LOSE!!!");
        }
    }
}
```
Stack vs Heap diagram:

![_Stack vs Heap_ (1)](https://github.com/user-attachments/assets/fd0409bb-5263-412c-a259-759a5db6380f)

I forgot to explicitely include it in the diagram, but the memory in the Stack will automatically be deallocated once the method returns, and the memory in the heap will be periodically deallocated based on its complex age system and the garbage collection via the JVM.

