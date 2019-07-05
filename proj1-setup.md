###  Documentation to setup your application


#### assuming the following architechture, Doc has been made. 

![image](https://user-images.githubusercontent.com/52474652/60711645-f6d75880-9f32-11e9-877f-0e4362a07439.png)

#### 1. Install and start Web Server.

"""
$sudo yum install httpd -y
$sudo systemctl enable httpd
$sudo systemctl start httpd
"""

##### Configure Web Server. 

'''

$sudo cat /etc/httpd/conf.d/studentapp.conf
ProxyPass "/student"  "http://localhost:8080/student"
ProxyPassReverse "/student"  "http://localhost:8080/student"

$sudo wget https://raw.githubusercontent.com/devopsdordie/project-1-documentation/master/httpd-index.html -O /var/www/html/index.html

$sudo systemctl restart httpd
'''

