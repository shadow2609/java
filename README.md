Package

1.	Create a package named "Presidency". Under this create two packages named "Employee" and "Student". Under the employee package create a class called "EmployeeDetails" having required member fields and methods. Under the Student package create a class called "StudentDetails" having required member fields and methods. Demonstrate the above by creating objects of StudentDetails and EmployeeDetails inside another class which resides in another package.Hint: You can assume the relevant fields and methods to be written inside the EmployeeDetails and StudentDetails class.


//Presidency.java

package presidency;

import presidency.employee.EmployeeDetails; import presidency.student.StudentDetails;

public class Presidency {

public static void main(String[] args) {
EmployeeDetails empDetails[] = new EmployeeDetails[5]; StudentDetails stuDetails[] = new StudentDetails[5]; for(int i =0; i<5;i++){
empDetails[i] = new EmployeeDetails(); empDetails[i].setEmployeeDetails();
}
for(int i=0;i<5;i++){
stuDetails[i] = new StudentDetails(); stuDetails[i].setStudentDetails();
}
for(int i=0;i<5;i++) empDetails[i].getEmployeeDetails();

for(int i=0;i<5;i++) stuDetails[i].getStudentDetails();

}

}

//EmployeeDetails.java package presidency.employee; import java.util.Scanner; public class EmployeeDetails {
String empName; int empId;
 
long empPhoneNumber;
Scanner scan = new Scanner(System.in); public void setEmployeeDetails(){
System.out.println("Enter the name of the Employee"); empName = scan.nextLine(); System.out.println("Enter the ID of the Employee"); empId = scan.nextInt();
System.out.println("Enter the phone number of the Employee"); empPhoneNumber = scan.nextLong();
}

public void getEmployeeDetails(){ System.out.println("Emp Id: "+empId); System.out.println("Emp Name: "+ empName);
System.out.println("Emp Phone Number: "+ empPhoneNumber);
}
}


//StudentDetails.java package presidency.student; import java.util.Scanner;
public class StudentDetails { String studentId;
String studentName; int semester;
Scanner scan = new Scanner(System.in); public void setStudentDetails(){
System.out.println("Enter the studnet's Id"); studentId = scan.nextLine(); System.out.println("Enter the name of the Student"); studentName = scan.nextLine();
System.out.println("Enter the semester the student is in"); semester = scan.nextInt();
}
public void getStudentDetails(){ System.out.println("Student Id:"+ studentId); System.out.println("Student's Name: "+ studentName); System.out.println("Semester :"+ semester);
}
}
 
Packages & Interface

2.	Tom is participating in a coding contest, he will win the contest if he performs the following task: Design and develop an application for Banking in Java using the concept of Interface. Follow the following instructions for developing the application.
a.	Create an interface IAccount which contains the functions such as balanceEnquiry(int accountNumber), depositAmount(int AccountNumber) and withdrawAmount(int AccountNumber) in package pkgintf.
b.	Create a class Account which implements IAccount in package pkgbase.
c.	Create a class SavingsAccount which inherits Account class in package pkgder
d.	Create a class CurrentAccount which inherits Account class in package pkgder
e.	Include a createAccount() method that generates account number in sequence and another method showAccountDetails() to display the account information.
f.	Create a Banking in package pkgtest to demonstrate the application using a menu driven program which gives the choices to operate. Create array for both types of accounts and manage the same.

//IAccount.java

package pkgintf;

public interface IAccount {
public void depositAmount(int accountNumber); public void balanceEnquiry(int accountNumber); public void withdrawAmount(int accountNumber);
}

//Banking.java //Main package banking; import java.util.Scanner;
import pkgbase.Account; import pkgder.CurrentAccount; import pkgder.SavingsAccount;

public class Banking {
public static int saCount=0; public static int caCount=0;
public static void main(String[] args) { Scanner scan = new Scanner(System.in);
SavingsAccount savingsAccount[] = new SavingsAccount[10];
CurrentAccount currentAccount[] = new CurrentAccount[10]; int choice;
int ch=0;
boolean contBanking = true;
 
while(contBanking){ do{
System.out.println("Create Account 1. Saving Account 2. Current Account 3.
More Options");
choice = scan.nextInt(); switch(choice){
case 1: savingsAccount[saCount]= new SavingsAccount(); savingsAccount[saCount].createAccount(); saCount++;
break;
case 2: currentAccount[caCount] = new CurrentAccount(); currentAccount[caCount].createAccount(); caCount++;
break;
}

}while(choice<=2); do{
int account=0;
System.out.println("1. Savings Acc Deposit 2. Savings Acc Withdraw 3.
Savings Acc BalanceEnquiry 4.Back"); System.out.println("Enter your choice of Banking"); ch = scan.nextInt();
if(ch<=3){
System.out.println("Enter the Account Number"); account = scan.nextInt();
}
switch(ch){
case 1: for(int i=0;i<saCount;i++){ savingsAccount[i].depositAmount(account);
}
break;
case 2: for(int i=0;i<saCount;i++){ savingsAccount[i].withdrawAmount(account);
}
break;
case 3: for(int i=0;i<saCount;i++){ savingsAccount[i].balanceEnquiry(account);
}
break;
}
}while(ch<=3);


do{
int account=0;
System.out.println("1. Current Acc Deposit 2. Current Acc Withdraw 3.
Current Acc BalanceEnquiry 4.Back"); System.out.println("Enter your choice of Banking"); ch = scan.nextInt();
 
if(ch<=3){
System.out.println("Enter the Account Number"); account = scan.nextInt();
}

switch(ch){
case 1: System.out.println("Number of CA "+caCount); for(int i=0;i<caCount;i++){
currentAccount[i].depositAmount(account);
}
break;
case 2: for(int i=0;i<caCount;i++){ currentAccount[i].withdrawAmount(account);
}
break;
case 3: for(int i=0;i<caCount;i++){ currentAccount[i].balanceEnquiry(account);
}
break;
}
}while(ch<=3);

System.out.println("Would you like to continue ?? Input 1 to continue... Any other to exit");
int num = scan.nextInt(); if(num!=1)
contBanking = false;
}
}

}




//Account.java
package pkgbase; import java.util.Scanner;
import pkgintf.IAccount;

public class Account implements IAccount { protected int accountNumber;
protected String accountHolderName; protected long accountBalance; protected double rateOfInterest; protected boolean overdraft;

Scanner scan = new Scanner(System.in);
 
public void showAccountDetails(){ System.out.println("Account Number :" + accountNumber);
System.out.println("Account Holder Name :"+ accountHolderName); System.out.println("Account Balance :" + accountBalance); System.out.println("Rate of Interest for your Acc : " +rateOfInterest); if(overdraft)
System.out.println("Overdraft Allowed"); else{
System.out.println("Overdraft not allowed");
}
}
@Override
public void depositAmount(int accountNumber) { if(accountNumber==this.accountNumber){
System.out.println("Enter amount to be deposited"); int amount = scan.nextInt();
accountBalance +=amount;
}
}

@Override
public void balanceEnquiry(int accountNumber) { if(accountNumber == this.accountNumber)
System.out.println("Balnce in Account"+ accountBalance);
}

@Override
public void withdrawAmount(int accountNumber) { if(accountNumber == this.accountNumber){
System.out.println("Enter the amount to withdraw"); int amount = scan.nextInt();
if(this.accountNumber<50000 && amount<=accountBalance){ accountBalance = accountBalance-amount; System.out.println("Balance in Account" + accountBalance);
 
}
else{

"+accountBalance);
}
 


System.out.println("Not enough Balance, your balance is
 
if(this.accountNumber>=50000){ accountBalance = accountBalance-amount;
System.out.println("Balance in Account" + accountBalance);
}

}
}

}



//CurrentAccount.java
 
package pkgder;

import java.util.Scanner; import pkgbase.Account;


public class CurrentAccount extends Account{ String businessName;
static int accNumGen = 50000;
Scanner scan = new Scanner(System.in); public CurrentAccount() {
rateOfInterest = 0; overdraft = true;
}
public void createAccount(){
Scanner scan = new Scanner(System.in); accountNumber = accNumGen++; System.out.println("Enter the Account Holder Name"); accountHolderName = scan.nextLine(); showAccountDetails();
}

}


//SavingsAccount.java

package pkgder;

import java.util.Scanner; import pkgbase.Account;

public class SavingsAccount extends Account{ static int accnumGen = 10000;
public SavingsAccount() { rateOfInterest = 5.5; overdraft = false;
}

public void createAccount(){
Scanner scan = new Scanner(System.in); accountNumber = accnumGen++; System.out.println("Enter the Account Holder Name"); accountHolderName = scan.nextLine(); showAccountDetails();
}

}
 
Exception Handling

3.	Shyam’s teacher asked him to submit an assignment on division of integers , he wrote a java program to complete the assignment, his program abruptly ended at a condition. Identify the condition where Shyama program abruptly ended and handle the condition using suitable measures.

package shyamassignment; import java.util.Scanner;

public class ShyamAssignment {

public static void main(String[] args) { Scanner scan = new Scanner(System.in);

int choice =1;
while(choice ==1){
System.out.println("Please input any number & a divisor to divide "); double number = scan.nextInt();
double div = scan.nextInt();

try{
double result = number / div; System.out.println("result is: "+ result);
}catch(ArithmeticException e){
System.out.println("Kindly input Another Divisor,You are trying to divide
by Zero");
}

System.out.println("Try Again? Input 1 for yes.."); choice = scan.nextInt();

}
}

}
 
User Defined Exception

4.	A stack is a basic data structure that can be logically thought of as a linear structure. Two operations that can be performed on a Stack are: Push operation which inserts an element into the stack. Pop operation which removes the last element that was added into the stack. It follows Last In First Out(LIFO) Order. Write a menu driven program in Java to perform the operations on an IntegerStack. Create custom exceptions to deal with the following situations


1.“EmptyStackException”, while trying to access from an empty stack. 2.“FullStackException” while trying to insert to a full stack.


package stack;

import java.util.Scanner;

class FullStackException extends Exception{ int size;

public FullStackException() {
}

public FullStackException(int size) { this.size = size+1;
}
public String toString(){
return "FullStackException: The number of elements in the stack is : "+size+" Can't insert";
}

}
class EmptyStackException extends Exception{ int size;
public EmptyStackException() {
}

public EmptyStackException(int size) { this.size = size;
}
public String toString(){
return "EmptyStackException: The number of elements in the stack is : "+ (size+1);
}

}

public class Stack {
 
int top=-1;
final int maxElements = 3;
int numberStack[] = new int[maxElements];

public void push(int element){ try{
if(top==maxElements-1){
throw new FullStackException(top);
}
else{
numberStack[++top] = element;
}
}catch(FullStackException fse){ System.out.println(fse);
}

}
public void pop(){ int element=0; try{
if(top==-1){
throw new EmptyStackException(top);
}
else{
System.out.println("Popped item is "+ numberStack[top--]);
}

}catch(EmptyStackException ese){ System.out.println(ese);
}

}

public void display(){ try{
if(top==-1){
throw new EmptyStackException(top);
}
for(int i = top; i>=0 ; i--){ System.out.println(numberStack[i]);
}
}catch(EmptyStackException ese){ System.out.println(ese);
}

}
public static void main(String[] args) { int choice =0;
Scanner scan = new Scanner(System.in); Stack stack = new Stack();
do{
 
System.out.println("1. Push 2.Pop 3.Display 4. Exit"); System.out.println("Enter your choice");
choice = scan.nextInt(); switch(choice){

case 1: System.out.println("Enter the element"); int element = scan.nextInt(); stack.push(element);
break;

case 2: stack.pop(); break;

case 3: System.out.println("Items in the stack are"); stack.display();
break;
}

}while(choice<=3);
}

}
