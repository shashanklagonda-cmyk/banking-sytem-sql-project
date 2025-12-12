# banking-sytem-sql-project
mysql-banking-system
The Banking Management System is a simple SQL-based project developed to simulate core banking operations. It allows managing customers, accounts, and transactions while demonstrating practical use of relational databases, SQL queries, stored procedures, and constraints.



Key Objectives
##Customer Management: Efficiently store and manage customer information, ensuring data integrity and security.

##Account Management: Enable creation, modification, and closure of bank accounts with proper validations.

##Transaction Handling: Facilitate deposits, withdrawals, and fund transfers with accurate recording and balance checks.



Advantages
Data Management: Centralized storage of customer and account information.

Accuracy: Automated calculations reduce human error in transactions.

Efficiency: Quick processing of deposits, withdrawals, and transfers.

Transparency: Maintains detailed transaction history for auditing.

Learning Tool: Provides hands-on practice with SQL, stored procedures, and relational database design.



Disadvantages
Limited Interface: Works mainly via MySQL CLI or Workbench; no GUI for end-users.

Scalability: Not designed for large-scale banking operations.

Security: Lacks advanced authentication and encryption features.

Manual Maintenance: Requires manual script execution for some operations.



Working Flow
Customer Management: Add or update customer details.

Account Creation: Link new accounts to customers with initial balance.

Transactions: Perform deposits, withdrawals, and transfers.

Transaction Logging: Record each transaction in the transactions table.

Balance Check: Validate account balance before withdrawal or transfer.

Reporting: Generate statements or view transaction history.


-- Step 1: Create and use database

CREATE DATABASE bankingSystem; USE bankingSystem;

-- Step 2: Create Account Table

mysql> create table accounts (accountnum int(20) primary key,cname varchar(30),
gender enum ('male','female'),actype enum('withdraw','deposite'),currbal int(40));

-- Step 3: Insert Sample Data

mysql> insert into accounts values (11110,'pooja','female','current',200000),
(11111,'suresh','male','savings',50000),(11112,'ramesh','male','savings',80000),
(11113,'abhishek','male','savings',100000),(11114,'virat','male','savings',120000),
(11115,'rohit','male','savings',140000),(11116,'dhoni','male','savings',150000),
(11117,'akshata','female','savings',160000),(11118,'sanjana','female','current',170000),
(11119,'sneha','female','current',180000),(11121,'rohan','male','current',210000),
(11122,'nikhil','male','current',220000),(00013,'sanji','male','current',70000),
(11124,'zoro','male','current',20000),(11125,'luffy','male','current',40000);


-- Step 4: Create Transaction Table
mysql> create table transactions(tid int(20) primary key,accountnum int(30),
transactiontype enum('withdraw','deposite'),amount int(30),transactiondate date);


-- Step 5: Insert Sample Transactions

mysql> insert into accounts values (11110,'pooja','female','current',200000),
(11111,'suresh','male','savings',50000),(11112,'ramesh','male','savings',80000),
(11113,'abhishek','male','savings',100000),(11114,'virat','male','savings',120000),
(11115,'rohit','male','savings',140000),(11116,'dhoni','male','savings',150000),
(11117,'akshata','female','savings',160000),(11118,'sanjana','female','current',170000),
(11119,'sneha','female','current',180000),(11121,'rohan','male','current',210000),
(11122,'nikhil','male','current',220000),(00013,'sanji','male','current',70000),
(11124,'zoro','male','current',20000),(11125,'luffy','male','current',40000);



-- Step 6: Queries with Output

1. Retrieve all customer names who have a balance greater than 50,000.
mysql> select cname as custemer_name,currbal as balance from accounts where currbal>50000;


2. Display account number, customer name, and account type of all customers having SAVINGS accounts.
mysql> select accountnum as account_number,cname as costemer_name,actype as account_type from accounts where actype='savings';


3. List all transactions made in the current month.
mysql> select * from transactions where month(transactiondate)=month(now());


4. Show customers who have not made any transactions yet.
mysql> select t1.cname from accounts as t1 inner join transactions as t2 on t1.accountnum=t2.accountnum where t2.tid is null;


5. Display the top 3 customers with the highest account balance.
mysql> select cname as costemer_name,currbal as current_balance  from accounts order by currbal desc limit 3;


6. Retrieve all transactions where the amount is greater than 10,000.
mysql> select tid as trans_id,accountnum as acc_num,amount from transactions where amount>10000;


7. Show the total balance of all accounts combined.
mysql> select sum(currbal) as costemers_totalbal from accounts;


8. List customers along with their total deposited amount.
mysql> select t1.cname as costemer_name,t1.currbal+t2.amount from accounts as t1 join transactions
as t2 on t1.accountnum=t2.accountnum where transactiontype='deposite';


9. Find customers who made a withdrawal of more than 5,000.
mysql> select cname as costemer_name,transactiontype as type_of_transactions,amount from accounts 
as t1 right join transactions as t2 on t1.accountnum=t2.accountnum where t2.transactiontype='withdraw' and t2.amount>5000;


10. Display the most recent transaction date for each account.
mysql> select accountnum,max(transactiondate) from transactions group by accountnum;


11)Retrieve the number of transactions each customer has made.
mysql> select a.cname as costemer_name,count(t.accountnum) as num_of_transaction from transactions t join
accounts a on t.accountnum=a.accountnum group by a.cname;


12)List customers who have both SAVINGS and CURRENT accounts (if allowed).
mysql> select cname as costemer_name from accounts where actype='current' and actype='savings';



13) Find all accounts created by customers whose name starts with 'P'.
mysql> select cname as costemer_name,accountnum as account_number from accounts where cname like('p%');


14) Retrieve customers sorted by their account balance in descending order
mysql> select cname as costemer_name,currbal as current_balance from accounts order by currbal desc;


15) Display the average account balance per account type
mysql> select actype as account_type,avg(currbal)as avg_of_curbalance from accounts group by actype;





Conclusion


The Banking Management System demonstrates fundamental banking operations using MySQL, providing a practical approach to managing customers, accounts, and transactions. It emphasizes database design, relational integrity, and the use of stored procedures for automation. While it is suitable for learning and small-scale simulations, it highlights the importance of accuracy, transparency, and structured data management in real-world banking. This project serves as a solid foundation for building more advanced banking applications with enhanced security, scalability, and user interfaces.












