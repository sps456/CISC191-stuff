## CISC 192 Honors Project: The Ultimate Project
I have included a video showcase of the code and some implimentations of it, as well as the entirety of the code itself.
Video Demonstration of Code:
https://drive.google.com/file/d/1mf6ayRMvSwmTKmD2ZxSZ--ienCz5vEgr/view?usp=sharing 

Code:

``` c++
#include <iostream>
#include <iomanip>
#include <vector>
#include <set>
#include <string>
#include <fstream>
#include <cmath>
using namespace std;

class Account {
protected:
    string ID;
    double balance;
    double interestRate;
public:
    double getBalance() {
        return balance;
    }
    virtual void withdrawl(double amount) {
        if (amount <= balance) {
            balance -= amount;
            cout << "$" << amount << " withdrawl successful. Your new account balance is $" << balance << endl;
        }
        else {
            cout << "Unable to. You only have $" << balance << " in your account.\n";
        }
    }
    void deposit(double amount) {
        balance += amount;
        cout << "Deposit successful. Your new account balance is $" << balance << endl;
    }
    double calculateInterest() {
        return balance * interestRate;
    }
    virtual void transferFunds(Account b, double amount) {
        if (amount <= balance) {
            balance -= amount;
            b.deposit(amount);
            cout << "Transfer successful.\n";
        }
        else {
            cout << "Transfer unsuccessful. You only have $" << balance << " in your account.\n";
        }
    }
    Account() {
    }
    virtual void passTime() {
        balance += this->calculateInterest();
    }
};

class SavingsAccount : public Account{ 
private:
    bool firstTransfer;
public:
    SavingsAccount(string id, double startingBalance) {
        balance = startingBalance;
        ID = id;
        interestRate = .0375;
        firstTransfer = true;
    }
    void withdrawl(double amount) override {
        if (balance >= 25) {
            if (amount <= balance) {
                balance -= amount;
                cout << "$" << amount << " withdrawl successful. Your new account balance is $" << balance << endl;
            }
            else {
                cout << "Withdrawl unsuccessful. You only have $" << balance << " in your account.\n";
            }
        }
        else {
            cout << "This account is inactive. Maintain a balance of $25 or more to reactivate it.\n";
        }
    }
    void transferFunds(Account b, double amount) override{
        if (amount + 1 <= balance) {
            if (!firstTransfer) {
                balance--;
            }
            balance -= amount;
            b.deposit(amount);
            cout << "Transfer successful.\n";
            firstTransfer = false;
        }
        else {
            cout << "Transfer unsuccessful. You only have $" << balance << " in your account.\n";
        }
    }
};

class CheckingAccount : public Account {
private:
    bool firstCheck;
    double fees;
public:
    CheckingAccount(string id, double startingBalance) {
        ID = id;
        balance = startingBalance;
        interestRate = .025;
        firstCheck = true;
        fees = 0;
    }
    void writeCheck(double amount) {
        if (!firstCheck) {
            balance -= .1;
        }
        if (amount <= balance) {
            balance -= amount;
        }
        else {
            cout << "WARNING! Your balance is insufficient to pay this check. You have recieved a $15 fee.\n";
            fees += 15;
        }
    }
    void passTime() override {
        if (balance >= 5) {
            balance -= 5;
        }
        else {
            cout << "WARNING! You were unable to pay your monthly service fee. Pay up soon or we forclose your house\n";
        }
        if (balance >= fees) {
            balance -= fees;
        }
        else {
            cout << "WARNING! You have past due fees. Pay up soon or we forclose your house\n";
        }
        balance += this->calculateInterest();
    }

};

class Employee {
private:
    string name;
    string ssn;
    double wage;
    int ID;
    string department;
    string dateHired;
public:
    Employee(string n, string social, double wg, int id, string dept, string date) {
        name = n;
        ssn = social;
        wage = wg;
        ID = id;
        department = dept;
        dateHired = date;
    }
    Employee() {
    }
    void setName(string n) {
        name = n;
    }
    string getName() {
        return name;
    }
    void setSSN(string n) {
        ssn = n;
    }
    string getSSN() {
        return ssn;
    }
    void setWage(double w) {
        wage = w;
    }
    double getWage() {
        return wage;
    }
    int getID() {
        return ID;
    }
    void setDepartment(string n) {
        department = n;
    }
    string getDepartment() {
        return department;
    }
    void setDateHired(string n) {
        dateHired = n;
    }
    string getDateHired() {
        return dateHired;
    }
};

vector<vector<int>> OddSquare(int n) {
        vector<vector<int>> square(n, vector<int>(n, 0));
        int i = n / 2;
        int j = n - 1;
        for (int num = 1; num <= n * n; num++) {
            square[i][j] = num;
            if (num % n == 0) {
                j--;
            }
            else {
                i--;
                j++;
            }
            i += n;
            i %= n;
            j += n;
            j %= n;
        }
        return square;
}

int main()
{
    int selection = 0;
    while (selection != -1) {
        cout << "Please select your task: Enter 1 for Banking, 2 for Employee List, or 3 for Magic Square. Enter -1 to exit the program" << endl;
        cin >> selection;
        if (selection == 1) {
            cout << "You have selected Banking Services\n";
            string id;
            double startingSavings;
            double startingChecking;
            cout << "Please enter a banking ID in the form \"NAME-SSN\" and a starting amount for your savings and checking account.\n";
            cin >> id >> startingSavings >> startingChecking;
            SavingsAccount save = SavingsAccount(id, startingSavings);
            CheckingAccount check = CheckingAccount(id, startingChecking);
            cout << "Here is a display of some of the classes methods:\n";
            save.withdrawl(20);
            check.writeCheck(15);
            save.transferFunds(check, 10);
            check.transferFunds(save, 5);
            save.passTime();
            check.passTime();
            cout << "After these transactions take place, your final savings balance is $" << save.getBalance();
            cout << " and your final checking balance is $" << check.getBalance() << endl;

        }
        else if (selection == 2) {
            cout << "You have selected Employee List\n";
            int choice = 0;
            string name, ssn, department, dateHired, filename;
            int ID, index;
            double wage;
            Employee recruit;
            vector<Employee> employeeList;
            set<int> idList = {};
            ofstream outFS;
            ifstream inFS;
            cout << "Enter 1 to add a new employee to the list\n";
            cout << "Enter 2 to search for an existing employee in the list\n";
            cout << "Enter 3 to print the entire list\n";
            cout << "Enter 4 to edit an employees information\n";
            cout << "Enter 5 to remove an employee from the list\n";
            cout << "Enter 6 to save your list to an external file\n";
            cout << "Enter 7 to import an employee list from an external file\n";
            cout << "Enter -1 to exit the Employee List task\n";
            while (choice != -1) {
                cout << "What would you like to do with your employee list?\n";
                cin >> choice;
                switch (choice) {
                case 1:
                    if (employeeList.size() < 100) {
                        cout << "Please enter your employees name, ssn, hourly wage, unique ID number, department, and date of hire (include no spaces)\n";
                        cin >> name >> ssn >> wage >> ID >> department;
                        cin >> dateHired;
                        while (idList.count(ID) == 1) {
                            cout << "That ID is already in use. Please enter a different ID\n";
                            cin >> ID;
                        }
                        recruit = Employee(name, ssn, wage, ID, department, dateHired);
                        employeeList.push_back(recruit);
                        idList.insert(ID);
                        cout << "Employee successfully added to list\n";
                    }
                    else {
                        cout << "Employee List can only contain 100 elements. Please remove an element before adding a new one\n";
                    }
                    break;

                case 2:
                    cout << "Please enter the ID of the employee you would like to search for:\n";
                    cin >> ID;
                    if (idList.count(ID) == 1) {
                        for (int i = 0; i < employeeList.size(); i++) {
                            if (employeeList.at(i).getID() == ID) {
                                index = i;
                            }
                        }
                        recruit = employeeList.at(index);
                        cout << "Employee found! Printing information...\n";
                        cout << "Name : " << recruit.getName() << "\tSSN: " << recruit.getSSN() << "\tWage: " << recruit.getWage() << "\tID: " << ID << "\tDepartment: " << recruit.getDepartment() << "\tHire Date: " << recruit.getDateHired() << endl;
                    }
                    else {
                        cout << "Employee not found\n";
                    }
                    break;
                case 3:
                    cout << "Printing Employee List...\n";
                    cout << left << setw(15) << "Name" << setw(10) << "SSN" << setw(10) << "Wage" << setw(10) << "ID" << setw(15) << "Department" << setw(12) << "Hire Date\n";
                    for (Employee e : employeeList) {
                        cout << left << setw(15) << e.getName() << setw(10) << e.getSSN() << setw(10) << e.getWage() << setw(10) << e.getID() << setw(15) << e.getDepartment() << setw(12) << e.getDateHired() << endl;
                    }
                    break;
                case 4:
                    cout << "Enter ID of employee you would like to update the information of:\n";
                    cin >> ID;
                    for (int i = 0; i < employeeList.size(); i++) {
                        if (employeeList.at(i).getID() == ID) {
                            index = i;
                        }
                    }
                    cout << "Enter in a new name, ssn, wage, department, and hire date. Enter -1 if you would like to keep an element the same\n";
                    cin >> name >> ssn >> wage >> department >> dateHired;
                    if (name != "-1") {
                        employeeList.at(index).setName(name);
                    }
                    if (ssn != "-1") {
                        employeeList.at(index).setSSN(name);
                    }
                    if (wage != -1) {
                        employeeList.at(index).setWage(wage);
                    }
                    if (department != "-1") {
                        employeeList.at(index).setDepartment(department);
                    }
                    if (dateHired != "-1") {
                        employeeList.at(index).setDateHired(dateHired);
                    }
                    break;
                case 5:
                    cout << "Enter the ID of the employee you would like to remove:\n";
                    cin >> ID;
                    if (idList.count(ID) == 1) {
                        for (int i = 0; i < employeeList.size(); i++) {
                            if (employeeList.at(i).getID() == ID) {
                                index = i;
                            }
                        }
                        employeeList.erase(employeeList.begin() + index);
                        idList.erase(ID);
                        cout << "This employee has been terminated\n";
                    }
                    else {
                        cout << "Can not find an employee with this ID\n";
                    }
                    break;
                case 6:
                    cout << "Enter the name of the file you would like to write to:\n";
                    cin >> filename;
                    outFS.open(filename + ".txt");
                    if (outFS.is_open()) {
                        for (int i = 0; i < employeeList.size() - 1; i++) {
                            Employee e = employeeList.at(i);
                            outFS << e.getName() << "\t" << e.getSSN() << "\t" << e.getWage() << "\t" << e.getID() << "\t" << e.getDepartment() << "\t" << e.getDateHired() << "\t\n";
                        }
                        outFS << employeeList.at(employeeList.size() - 1).getName() << "\t" << employeeList.at(employeeList.size() - 1).getSSN() << "\t" << employeeList.at(employeeList.size() - 1).getWage() << "\t" << employeeList.at(employeeList.size() - 1).getID() << "\t" << employeeList.at(employeeList.size() - 1).getDepartment() << "\t" << employeeList.at(employeeList.size() - 1).getDateHired();

                        outFS.close();
                        cout << "Employee List information has been output to " << filename << ".txt\n";
                    }
                    else {
                        cout << "Unable to open file\n";
                    }
                    break;
                case 7:
                    cout << "Enter the name of the file you wish to read from:\n";
                    cin >> filename;
                    inFS.open(filename + ".txt");
                    if (inFS.is_open()) {
                        while (!inFS.fail()) {
                            inFS >> name >> ssn;
                            inFS >> wage;
                            inFS >> ID;
                            inFS >> department >> dateHired;
                            if (!inFS.fail()) {
                                recruit = Employee(name, ssn, wage, ID, department, dateHired);
                                employeeList.push_back(recruit);
                                idList.insert(ID);
                            }
                        }
                        inFS.close();
                        cout << "Employee List information read from file\n";
                    }
                    else {
                        cout << "Unable to open file\n";
                    }
                    break;
                case -1:
                    break;
                default:
                    cout << "Invalid choice. Try again\n";
                    break;
                }
            }
        }
        else if (selection == 3) {
            cout << "You have selected Magic Square\n";
            int n;
            cout << "Please enter the degree of your magic square (must be between 3 and 15 inclusive):\n";
            cin >> n;
            if (n % 2 != 0) {
                vector<vector<int>> square = OddSquare(n);
                int random = (rand() % 11) + 1;
                for (int i = 0; i < n; i++) {
                    for (int j = 0; j < n; j++) {
                        cout << random * square[i][j] << " ";
                    }
                    cout << endl;
                }
            }
            else if (n % 4 == 0) {
                vector<vector<int>> square(n, vector<int>(n, 0));
                int i, j;
                for (i = 0; i < n; i++) {
                    for (j = 0; j < n; j++) {
                        square[i][j] = (n * i) + j + 1;
                    }
                }
                for (i = 0; i < n / 4; i++) {
                    for (j = 0; j < n / 4; j++) {
                        square[i][j] = (n * n + 1) - square[i][j];
                    }
                }
                for (i = 0; i < n / 4; i++) {
                    for (j = 3 * (n / 4); j < n; j++) {
                        square[i][j] = (n * n + 1) - square[i][j];
                    }
                }
                for (i = 3 * n / 4; i < n; i++) {
                    for (j = 0; j < n / 4; j++) {
                        square[i][j] = (n * n + 1) - square[i][j];
                    }
                }
                for (i = 3 * n / 4; i < n; i++) {
                    for (j = 3 * n / 4; j < n; j++) {
                        square[i][j] = (n * n + 1) - square[i][j];
                    }
                }
                for (i = n / 4; i < 3 * n / 4; i++) {
                    for (j = n / 4; j < 3 * n / 4; j++) {
                        square[i][j] = (n * n + 1) - square[i][j];
                    }
                }
                int random = (rand() % 11) + 1;
                for (i = 0; i < n; i++) {
                    for (j = 0; j < n; j++) {
                        cout << random * square[i][j] << " ";
                    }
                    cout << "\n";
                }
            }
            else {
                int innerDegree = n / 2;
                int squareSize = innerDegree * innerDegree;
                vector<vector<int>> A = OddSquare(innerDegree);
                vector<vector<int>> B = OddSquare(innerDegree);
                vector<vector<int>> C = OddSquare(innerDegree);
                vector<vector<int>> D = OddSquare(innerDegree);
                vector<vector<int>> M(n, vector<int>(n));

                for (int i = 0; i < innerDegree; ++i) {
                    for (int j = 0; j < innerDegree; ++j) {
                        M[i][j] = A[i][j];                  
                        M[i][j + innerDegree] = C[i][j] + squareSize * 2;   
                        M[i + innerDegree][j] = D[i][j] + squareSize * 3; 
                        M[i + innerDegree][j + innerDegree] = B[i][j] + squareSize;   
                    }
                }
                int m = (innerDegree - 1) / 2;
                for (int i = 0; i < innerDegree; ++i) {
                    for (int j = 0; j < m; ++j) {
                        swap(M[i][j], M[i + innerDegree][j]);
                    }
                }
                for (int i = 0; i < innerDegree; ++i) {
                    for (int j = 0; j < m - 1; ++j) {
                        swap(M[i][j + innerDegree + (innerDegree - m + 1)], M[i + innerDegree][j + innerDegree + (innerDegree - m + 1)]); // this needs careful index handling
                    }
                }
                for (int i = 0; i < innerDegree; i++) {
                    for (int j = 0; j < m - 1; j++) {
                        swap(M[i][innerDegree - j - 1], M[i + innerDegree][innerDegree - j - 1]); 
                    }
                }
                int random = (rand() % 11) + 1;
                for (int i = 0; i < n; i++) {
                    for (int j = 0; j < n; j++) {
                        cout << random * M[i][j] << " ";
                    }
                    cout << "\n";
                }
            }
        }
            else if (selection == -1) {
                break;
            }
            else {
                cout << "Invalid option! Enter 1 for Banking, 2 for Employee List, or 3 for Magic Square" << endl;
            }
        }
    }
```
