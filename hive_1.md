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

--->ther is two way loading the data one is local that we did above and other hdfs file path.

----> above in select command we are b=not getting the column name in result ciz we have the property in hive for that and command is
#command
set hive.cli.print.header=true;

now give select it will show the column  name also.
select * from department_data;

----> if we give drop the table then metadata will be erased and data from warehouse in hdfs will also be erased coz it was internal table.
#command
drop table department_data;
---> now give 
show tables;
you will see department_data is not there and now give
describe formatted department_data;
above one shows the meta data of table so here you will get table not found.

---> you can give this command in bash terminal to check is data is there or not you will not find anything.
hadoop fs -ls /user/hive/warehouse/hive_db.db

--------------------------------------------------------------------------------------------------
from here we go with hdfs path above was from local path

----> we will create the same table for practical purpose
#command
create table department_data
(dept_id int,
dept_name string,
manager_id int,
salary int
)
row format delimited
fields terminated by ','; 

--> loading data from hdfs path so the command is
#command to laod from hdfs path
load data inpath '/tmp/depart_data.csv' into table department_data;

--->path you can take from go to bash terminal give
hadoop fs -ls /tmp
you will path copy this only /tmp/depart_data.csv and paste  in inpath.
------------------------------------------------------------------------------------
#give select command and see the details again you will see.
select * from department_data;

----> now this is also the internal table coz we directong or giving any reference.(there will be seperate syntax that)
you can verify it from 
describe formatted department_data;
yo will see MANAGED_TABLE means internal table.

--------------------------------------------------------------------------------------
from here we will go with external table so
first go to bash terminal and create a new folder input_data in hadoop and put depart_data.csv inside thta folder commands are.

hadoop fs -mkdir /input_data/
hadoop fs -put depart_data.csv /input_data













