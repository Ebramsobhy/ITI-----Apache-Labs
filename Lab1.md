# Lab 1
### 1- Install Apache HTTP server. 
```
sudo yum install httpd
```
<div>
  <img src="https://user-images.githubusercontent.com/116510911/217589037-b8c054e0-c876-47aa-8552-6b26eced7712.png"/>
</div>

```
 service httpd start
```
<div>
  <img src="https://user-images.githubusercontent.com/116510911/217590866-b610bf83-1b46-4f4f-8f21-83cc61e10da5.png"/>
</div>

### 2- Create two simple html pages named “page1.html, page2.html” then use the suitable 
### directive to automatically redirect from localhost/page1.html to
### localhost/page2.html. 
Open this httpd.conf :
```
gedit /etc/httpd/conf/httpd.conf
```
And add :
```
<Directory /var/www/html/task2>
     Redirect /task2/page1.html /task2/page2.html
</Directory>
```
### 3- Ask for user name and password when accessing a directory. 

Make a directory and name it task3 and move inside this directory and write this command :
```
sudo htpasswd -c .pass ebram
```
After that go again to the httpd.conf and add :
```
<Directory /var/www/html/task3>
     AuthType basic
     AuthName "Please login"
     AuthUserFile /var/www/html/task3/.pass
     require valid-user
</Directory>
```
The result : 
<div>
  <img src="https://user-images.githubusercontent.com/116510911/217596383-daa14985-aa11-47a4-a083-394b8c7043de.png"/>
</div>

### 4-Apply authentication before downloading PDF files.
```
<FilesMatch \.pdf>
   AuthType basic
    AuthName "Please login"
    AuthUserFile /var/www/html/task4/.pass
    require valid-user
</FilesMatch>
```
The result :
<div>
  <img src="https://user-images.githubusercontent.com/116510911/217597461-4ba14212-82a9-4c98-b27a-2c3622d2494f.png"/>
</div>

### 5- Create a directory then allow access to one of your classmates only.
```
<Directory /var/www/html/task5>
    Allow from 192.168.1.10
    deny from all
    order deny,allow
</Directory>
```
The result :
<div>
  <img src="https://user-images.githubusercontent.com/116510911/217598098-897ff03a-1c37-4c24-85ee-1890474a1088.png"/>
</div>

### 6-Disable listing the directory content (hint use indexs)
```
<Directory /var/www/html/task6>
    Options - Indexes
</Directory>
```
The result :
<div>
  <img src="https://user-images.githubusercontent.com/116510911/217598972-38cc2649-d7f3-4d93-9501-4bbe0b4acb46.png"/>
</div>

### 7-Change the default index page to be default.html instead of index.html (use DirectoryIndex)
```
<IfModule dir_module>
    DirectoryIndex default.html
</IfModule>
```
The result :
<div>
  <img src="https://user-images.githubusercontent.com/116510911/217599704-b77d7664-0bd2-406d-a1e8-b5ee7cddfe8c.png"/>
</div>
