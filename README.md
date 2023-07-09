# Hive
always try to practice in neurolab -Hive
first commands- show databases;
imp question for interview-How many types of table we can create in Hive??
ans-internal table and external table(see notes)
#command to show all databases:
show databases;
#command to create new database
create database hive_db;
#to create table inside hive_db
first go inside hive_db
use hive_db;
------------------------------------
copy and paste from github repo of shashank and create one  file depart_data.csv
got to bash terminal and
ls (you will see depart_data.csv) is there
then copy this data inside hadoop as we discussed for the external table creation part
command in bash--> hadoop fs -ls /
hadoop fs -put depart_data.csv /tmp

now you can it is inside tmp directory
hadoop fs -ls /tmp

now come to the terminal
-------------------------------------------------------------------------------------------
#command to show tables
show tables;
#command to create table   
create table department_data
(dept_id int,
dept_name string,
manager_id int,
salary int
)
row format delimited
fields terminated by ',';                      ---->coz in file it is seperated by ','.

----> now we will load the data into above table from hdfs input path coz we pasted above from the local system coz there is two way to load data into hdfs path one by copying and second by inserting directly.

---->you can see the data in local system by giving command in bas terminal
ls
#command to show the detail of the table
describe department_data;
#command to show themore detail o0or granular details of the table
describe formatted department_data;
#inserting data frok local to table
load data local inpath 'file:///config/workspace/depart_data.csv' into table department_data;

-->inpath you can atke from first got to bash terminal give pwd(current directory) copy and paste like that found -config/workspace
--------------------------------------------------
file:///config/workspace/depart_data.csv paste it in ''.

--->now you can see the content of the table by
#select command
select * from department_data;

# you can check it is internal or external tbale by giving command in terminal.
describe formatted department_data;
--->you will see table type there here it is MANAGED_TABLE means it is internal table.




