# $${\color{orange} \textbf{Project}: \textbf{Student}  \ \textbf{App}}$$


**Installations:**

Launch EC2

Java-1.8

Tomcat

Git

RDS


**Security Group**

Allow Ports in security group: 22 = SSH 8080 = Tomcat 3306 = Mysql / Mariadb  80=http

**launch instance**

**connect to instance**

connect cli

**install java**

yum install java-1.8* -y 

**Install tomcat** 

 **Search tomcat 8 download on browser**


wget https://dlcdn.apache.org/tomcat/tomcat-9/v9.0.96/bin/apache-tomcat-9.0.96.tar.gz

tar -xvzf apache-tomcat-9.0.96.tar.gz -C /opt/
 
cd  apache-tomcat-8.5.99.zip 

cd bin 

[catalina.sh  -->this file is neccessary to start tomcat] 

chmod +x catalina.sh     [ give execute permission to file] 

Start

Stop
 
**Tomcat**

sh catalina.sh start   [ tomcat started ]

sh catalina.sh stop 

go to browser and public ip:8080

**SetUp Student Application**

yum install git -y 

git clone https://github.com/abhipraydhoble/Student-App-Project.git 

cd Student-App-Project 

**copt file from the git directrory to the tomcat**

cp Student-App-Project/student.war apache-tomcat-8.5.93/webapps/ 

cp Student-App-Project/mysql-connector.jar apache-tomcat-8.5.93/lib/ 


**Create Database in RDS**

**Go to RDS download mariadb-server using below command**

yum install mariadb105-server -y
systemctl start mariadb    
systemctl enable mariadb  
systemctl status mariadb

**LogIn to Database**

mysql -h "database-1.cxqukacgq5pj.us-east-1.rds.amazonaws.com"   -u admin -pPasswd123$
Note: replace rds-endpoint with actual endpoint value

show databases;
create database  studentapp;
use studentapp;

**Create Table in DB**
 
 CREATE TABLE if not exists students(student_id INT NOT NULL AUTO_INCREMENT,  
	student_name VARCHAR(100) NOT NULL,  
	student_addr VARCHAR(100) NOT NULL,   
	student_age VARCHAR(3) NOT NULL,      
	student_qual VARCHAR(20) NOT NULL,     
	student_percent VARCHAR(10) NOT NULL,   
	student_year_passed VARCHAR(10) NOT NULL,  
	PRIMARY KEY (student_id)  
);

**Logout from database:**
 exit

 
**Modify apache-tomcat/conf/context.xml file**

cd apache-tomcat-8.5.93/conf
vim context.xml
add below line [connection string] at line 21

 <Resource name="jdbc/TestDB" auth="Container" type="javax.sql.DataSource"
               maxTotal="100" maxIdle="30" maxWaitMillis="10000"
               username="USERNAME" password="PASSWORD" driverClassName="com.mysql.jdbc.Driver"
               url="jdbc:mysql://DB-ENDPOINT:3306/DATABASE"/>

**Change**
1.Username
2.Password
3.DB-ENDPOINT
4.DATABASE Name


**Start tomcat**


cd apache-tomcat-8.5.93/bin
./catalina.sh start or  sh catalina.sh start


**Googlehit**
 Public IP:8080/student
