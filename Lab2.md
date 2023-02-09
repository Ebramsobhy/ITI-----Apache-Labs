## Write RewriteCond and RewiteRules for :
### A- Deny access to http://localhost/page?queryString if queryString contains the string hack
Open the httpd.conf :
```
gedit /etc/httpd/conf/httpd.conf
```
And add : 
```
      RewriteCond "%{QUERY_STRING}" "hack"
      RewriteRule "." "-" [F]
```
### B- Remove the Query String.
```
      RewriteCond "%{QUERY_STRING}" ^(.+)$
      RewriteRule (.+)  $1?   [R]
```
### C- Rewrite URLs like http://localhost/page1?var=val to http://localhost/page2?var=val but do not rewrite if val isn't present
```
      RewriteCond "%{QUERY_STRING}" "^(.+)=(.+)$"
      RewriteRule  "^/page1$"  "/page2%1=%2"
```
### D- Take a URL of the form http://localhost/path?var=val and transform it into http://localhost/path/var/val
```
      RewriteCond "%{QUERY_STRING}" "^(.+)=(.+)$"
      RewriteRule   (.+)        $1/%1/%2? [R]
```
### E- Map http://localhost/example/one/two to http://localhost/something.cgi?arg=one&other=two
```
      RewriteRule ^/example/(.+)/(.+)$ /something.cgi?arg=$1&other=$2 [R]
```
