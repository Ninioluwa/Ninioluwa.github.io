
Let's 'GET' right into this!

The user interface for the application on the server:
![](/picoCTF/GET_aHEAD/assets/webpage.png)


There are two buttons that change the background color of the website to either blue or red

![](/picoCTF/GET_aHEAD/assets/blue_web_page.png)


One of the very first steps when testing a web application is to inspect the web page in the browser. This gives some insight on the source code of the application.

![](/picoCTF/GET_aHEAD/assets/inspect_code.png)

From the above picture, we can see that the application makes a **GET** request to **index.php**. 

Let's make use of burp suite to analyse the HTTP method better. The title of the challenge seems to give a hint, GET and HEAD are both HTTP methods.

  
The HTTP HEAD method makes requests to the server, similar to how you would make requests using the HTTP GET method. The main difference is that with HTTP HEAD, you only receive the headers of the web page from the server, without any actual content or body. [Read more on the HTTP HEAD request method](https://reqbin.com/Article/HttpHead)


#### Alrighty!

Now we know how the HTTP HEAD request works, let's get on with it!

First, we intercept the response.
```
GET /index.php? HTTP/1.1
Host: mercury.picoctf.net:47967
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/111.0.5563.65 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://mercury.picoctf.net:47967/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Connection: close

```


Now, let's send this to the repeater using `ctrl + r` , to modify the request method.

```
HEAD /index.php? HTTP/1.1
Host: mercury.picoctf.net:47967
Upgrade-Insecure-Requests: 1
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/111.0.5563.65 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://mercury.picoctf.net:47967/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Connection: close

```


Send the request and it goes 'aHEAD' to return the flag in the response.

``` FLAG
HTTP/1.1 200 OK
flag: ******
Content-type: text/html; charset=UTF-8

```


This was a pretty basic exercise. All we had to do was a bit of research and change the request method. 

### Well-done and Thanks for reading!