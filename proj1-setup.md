###  Documentation to setup your application


#### assuming the following architechture, Doc has been made. 

![image](https://user-images.githubusercontent.com/52474652/60711645-f6d75880-9f32-11e9-877f-0e4362a07439.png)

#### 1. Install and start Web Server.

```
$sudo yum install httpd -y
$sudo systemctl enable httpd
$sudo systemctl start httpd
```

##### Configure Web Server. 

```

$sudo cat /etc/httpd/conf.d/studentapp.conf
ProxyPass "/student"  "http://localhost:8080/student"
ProxyPassReverse "/student"  "http://localhost:8080/student"

$sudo wget https://raw.githubusercontent.com/devopsdordie/project-1-documentation/master/httpd-index.html -O /var/www/html/index.html

$sudo systemctl restart httpd
```

#### 2. Install and Start Tomcat Sever.

While seting up any application it is always a good practice to create a user and run the applicaiton using that user. 
For that we are going to use `student` user to run out student application. 

#### Add user and install java
```
$sudo useradd student
$sudo yum install java -y
```

#### Download and setup App server and run it as student user
```
$sudo su - student
student $ wget https://www.apache.org/dist/tomcat/tomcat-8/v8.5.42/bin/apache-tomcat-8.5.42.tar.gz.asc
student $tar -xf apache-tomcat-8.5.42.tar.gz
student $cd apache-tomcat-8.5.42/webapps
student $wget https://github.com/citb34/project-1-documentation/raw/master/studentapp.war -O webapps/student.war
student $vim  conf/context.xml

<Resource name="jdbc/TestDB" auth="Container" type="javax.sql.DataSource"
               maxActive="100" maxIdle="30" maxWait="10000"
               username="USERNAME" password="PASSWORD" driverClassName="com.mysql.jdbc.Driver"
               url="jdbc:mysql://RDS-ENDPOINT:3306/DATABASE"/>

#### Add the above content just before the last line, Last line ususally looks like  </Context>
#### Note: Replace USERNAME, PASSWORD, RDS-ENDPOINT, DATABASE with associated RDS valuses after creating it.
```

Switch back to CentOS user and run the following commands. 
```
#wget 

