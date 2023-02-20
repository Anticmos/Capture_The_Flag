# Hack TM 2023 – Blog

* **Category:** Web
* **Points:** 50 Points

## Challenge

> The text of 
> the challenge.
![Blog](blog_description.png?raw=true "Challenge - Blog")

## Solution
1. We are presented with a webpage that contains a registration and login page.

We quickly learn we have a cookie that looks like this:
```
Tzo0OiJVc2VyIjoyOntzOjc6InByb2ZpbGUiO086NzoiUHJvZmlsZSI6Mjp7czo4OiJ1c2VybmFtZSI7czoxOiIxIjtzOjEyOiJwaWN0dXJlX3BhdGgiO3M6Mjc6ImltYWdlcy9yZWFsX3Byb2dyYW1tZXJzLnBuZyI7fXM6NToicG9zdHMiO2E6MDp7fX0%3D
```
2. The cookie is URL + base64 encoded.
It looks like this once decoded.
```
O:4:"User":2:{s:7:"profile";O:7:"Profile":2:{s:8:"username";s:1:"1";s:12:"picture_path";s:27:"images/real_programmers.png";}s:5:"posts";a:1:{i:0;O:4:"Post":3:{s:5:"title";s:5:"title";s:7:"content";s:17:"$txt = exec("ls")";s:8:"comments";s:3:"txt";}}}
```
3. Upon investigating the source code that was shared along with the challenge we found that during the infrastructure setup the flag is copied to following directory.
```
FROM php:8.0-apache

COPY ./chal/html /var/www/html
COPY ./chal/db /sqlite3/db
COPY ./chal/flag.txt /02d92f5f-a58c-42b1-98c7-746bbda7abe9/flag.txt
RUN chmod -R 777 /sqlite3/
RUN chmod -R 777 /var/www/html/
```
4. We can have the ability to replace the "picture_path" in the cookie and replace that local file with the location of the flag. "/02d92f5f-a58c-42b1-98c7-746bbda7abe9/flag.txt"
5. The flag is returned as a base64 encoded image which we can decode.
![flag](flag.png?raw=true "flag")

