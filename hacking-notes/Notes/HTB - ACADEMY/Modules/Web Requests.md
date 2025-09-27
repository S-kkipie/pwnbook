---
tags:
  - "#MOC"
  - "#Module"
platform: "[[Hack The Box]]"
difficulty: Fundamental
tier: I
banner: "![[web-requests-banner.webp]]"
status: Incomplete
---

> [!danger]- Associated Certs
> [[HTB CJCA|HTB Certified Junior Cybersecurity Associate]]
> [[Bug Bounty Hunter]]
>[[CREST CPSA CRT]]
^faq

> [!faq]- Associated Paths
> [[Bug Bounty Hunter]]
> [[Cracking into Hack the Box]]
> [[Information Security Foundations]]
> [[SOC Analyst Prerequisites]]
> [[Junior Cybersecurity Analyst]]
^faq

> [!summary] Web Requests Summary
> This module introduces key fundamentals that must be mastered to be successful in information security. Understanding web requests is essential for understanding how web applications work, which is necessary before attempting to attack or secure any web application. This makes this module the very first step in web application penetration testing.
> 
This module will deliver these concepts through two main tools: `cURL` and the `Browser DevTools`. These tools are among the essential tools in any web penetration tester's arsenal, and this module will start you on the path to mastering them.
^summary

> [!FLag] In this module, we will cover:
> - An overview of the HyperText Transfer Protocol (HTTP)
>- An overview of the Hypertext Transfer Protocol Secure (HTTPS)
>- HTTP requests and responses and their headers
>- HTTP methods and response codes
>- Common HTTP methods such as GET, POST, PUT, and DELETE
>- Interacting with APIs

>[!tldr] Cheat Sheet
![[Web_Requests_Module_Cheat_Sheet.pdf]]
# Sections
## 1. HyperText Transfer Protocol (HTTP)
HyperText refers a text with links (URLs), this is an standard of client-server communication, HTTP is a protocol and uses the port `80` , through this protocol we can access to the World Wide Websites.
#### URL
Resources over HTTP are accessed via URL.
![[Pasted image 20250917123928.png]]
Here is what each component stands for:

|**Component**|**Example**|**Description**|
|---|---|---|
|`Scheme`|`http://` `https://`|This is used to identify the protocol being accessed by the client, and ends with a colon and a double slash (`://`)|
|`User Info`|`admin:password@`|This is an optional component that contains the credentials (separated by a colon `:`) used to authenticate to the host, and is separated from the host with an at sign (`@`)|
|`Host`|`inlanefreight.com`|The host signifies the resource location. This can be a hostname or an IP address|
|`Port`|`:80`|The `Port` is separated from the `Host` by a colon (`:`). If no port is specified, `http` schemes default to port `80` and `https` default to port `443`|
|`Path`|`/dashboard.php`|This points to the resource being accessed, which can be a file or a folder. If there is no path specified, the server returns the default index (e.g. `index.html`).|
|`Query String`|`?login=true`|The query string starts with a question mark (`?`), and consists of a parameter (e.g. `login`) and a value (e.g. `true`). Multiple parameters can be separated by an ampersand (`&`).|
|`Fragments`|`#status`|Fragments are processed by the browsers on the client-side to locate sections within the primary resource (e.g. a header or section on the page).|
#### HTTP Flow
![[Pasted image 20250917124119.png]]
When we access to an URL, first it resolve the DNS name, and after forward the request to the real server.
> [!note] 
> Our browsers usually first look up records in the local '`/etc/hosts`' file, and if the requested domain does not exist within it, then they would contact other DNS servers. We can use the '`/etc/hosts`' to manually add records to for DNS resolution, by adding the IP followed by the domain name.

When the client asks for the `/` path, the server return by default an index file and a `200 OK` code when everything is okay.

#### cURL
`{sh icon}curl` command is a cli tool which we can send HTTP request.
We can send a basic HTTP request to any URL by using it as an argument for cURL, as follows:

```shell-session ln:false
[!bash!]$ curl inlanefreight.com

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
...SNIP...
```

curl doesn't render HTML/CSS, it provides the response in raw format. We can save the result with the flag `-O` .
```shell-session ln:false
[!bash!]$ curl -O inlanefreight.com/index.html
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 464    0 464    0     0  17858      0 --:--:-- --:--:-- --:--:-- 18069
[!bash!]$ ls
index.html
```

#### Lab
Target(s): `<URL>`

1.  To get the flag, start the above exercise, then use cURL to download the file returned by '/download.php' in the server shown above.

```sh-session ln:false
 curl -O 94.237.55.43:58567/download.php -s     
 cat download.php                                                             
 HTB{64$!c_cURL_u$3r}
```

## 2.  Hypertext Transfer Protocol Secure (HTTPS)
One of the significant drawbags of HTTP are the security of the sended data, HTTP sends data in clean text, allowing intruders can read the request, this attack is called Man In The Middle (MiTM.
To counter this issue, HTTPS was created implementing a secure way to send data, HTTPS encrypt data and decrypt in the client-server communication.
#### HTTPS Overview
![[Pasted image 20250917141027.png]]

This is an example of an HTTP login request, we can see the user's password in plain text. This would be easy for someone intercepting the request and obtain the credentials.
In contrast, if someone tries to see an HTTPS requests, he see encrypted data like this:
![[Pasted image 20250917141634.png]]

Websites that enforce HTTPS can be identified through `https://` in their URL (e.g. https://www.google.com), as well as the lock icon in the address bar of the web browser, to the left of the URL:
![[Pasted image 20250917141830.png]]

>[!note] 
>Although the data transferred through the HTTPS protocol may be encrypted, the request may still reveal the visited URL if it contacted a clear-text DNS server. For this reason, it is recommended to utilize encrypted DNS servers (e.g. 8.8.8.8 or 1.1.1.1), or utilize a VPN service to ensure all traffic is properly encrypted.

#### HTTPS Flow
![[Pasted image 20250917142003.png]]

If we type `http://` instead of `https://` to visit a website that enforces HTTPS, the browser attempts to resolve the domain and redirects the user to the webserver hosting the target website. A request is sent to port `80` first, which is the unencrypted HTTP protocol. The server detects this and redirects the client to secure HTTPS port `443` instead. This is done via the `301 Moved Permanently` response code, which we will discuss in an upcoming section.

> [!note] 
> Depending on the circumstances, an attacker may be able to perform an HTTP downgrade attack, which downgrades HTTPS communication to HTTP, making the data transferred in clear-text. This is done by setting up a Man-In-The-Middle (MITM) proxy to transfer all traffic through the attacker's host without the user's knowledge. However, most modern browsers, servers, and web applications protect against this attack.
^important
#### cURL for HTTPS
We may face such an issue when testing a local web application or with a web application hosted for practice purposes, as such web applications may not yet have implemented a valid SSL certificate. To skip the certificate check with cURL, we can use the `-k` flag:

  Hypertext Transfer Protocol Secure (HTTPS)

```shell-session
Skkippie@htb[/htb]$ curl -k https://inlanefreight.com

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
...SNIP...
```

As we can see, the request went through this time, and we received the response data.

## 3. HTTP Requests and Responses
The client-server communication is made of request and responses like cURL and servers.
#### HTTP Request
![[Pasted image 20250917164107.png]]
The image above shows an HTTP GET request to the URL:

- `http://inlanefreight.com/users/login.html`

The first line of any HTTP request contains three main fields 'separated by spaces':

| **Field** | **Example**         | **Description**                                                                                                       |
| --------- | ------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `Method`  | `GET`               | The HTTP method or verb, which specifies the type of action to perform.                                               |
| `Path`    | `/users/login.html` | The path to the resource being accessed. This field can also be suffixed with a query string (e.g. `?username=user`). |
| `Version` | `HTTP/1.1`          | The third and final field is used to denote the HTTP version.                                                         |

The next set of lines contain HTTP header value pairs, like `Host`, `User-Agent`, `Cookie`, and many other possible headers. These headers are used to specify various attributes of a request. The headers are terminated with a new line, which is necessary for the server to validate the request. Finally, a request may end with the request body and data.

> [!note]
> HTTP version 1.X sends requests as clear-text, and uses a new-line character to separate different fields and different requests. HTTP version 2.X, on the other hand, sends requests as binary data in a dictionary form. 

#### HTTP Response
![[Pasted image 20250917164500.png]]

The first line of an HTTP response contains two fields separated by spaces. The first being the `HTTP version` (e.g. `HTTP/1.1`), and the second denotes the `HTTP response code` (e.g. `200 OK`).

#### cURL
With the flag `-v` we can see the request and the response.
```shell-session ln:false
Skkippie@htb[/htb]$ curl inlanefreight.com -v

*   Trying SERVER_IP:80...
* TCP_NODELAY set
* Connected to inlanefreight.com (SERVER_IP) port 80 (#0)
> GET / HTTP/1.1
> Host: inlanefreight.com
> User-Agent: curl/7.65.3
> Accept: */*
> Connection: close
> 
* Mark bundle as not supporting multiuse
< HTTP/1.1 401 Unauthorized
< Date: Tue, 21 Jul 2020 05:20:15 GMT
< Server: Apache/X.Y.ZZ (Ubuntu)
< WWW-Authenticate: Basic realm="Restricted Content"
< Content-Length: 464
< Content-Type: text/html; charset=iso-8859-1
< 
<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>

...SNIP...
```
>[!note] 
>The `-vvv` flag shows an even more verbose output. Try to use this flag to see what extra request and response details get displayed with it.

#### Browser DevTools
Modern browsers include developer tools (DevTools) for testing web apps, which are also useful for web penetration testing. This module explains how to use basic DevTools—especially the **Network** tab—to observe and analyze the HTTP requests and responses a browser makes when loading a site. DevTools can be opened with `Ctrl + Shift + I` or `F12` in Chrome or Firefox.
![[Pasted image 20250917164728.png]]

## 4.  HTTP Headers
Headers can have one or multiple values, appended after the header name and separated by a colon. We can divide headers into the following categories:

1. `General Headers`
2. `Entity Headers`
3. `Request Headers`
4. `Response Headers`
5. `Security Headers`

#### General Headers

[General headers](https://www.w3.org/Protocols/rfc2616/rfc2616-sec4.html) are used in both HTTP requests and responses. They are contextual and are used to `describe the message rather than its contents`.

| **Header**   | **Example**                           | **Description**                                                                                                                                                                                                                                                                                                                                                                           |
| ------------ | ------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Date`       | `Date: Wed, 16 Feb 2022 10:38:44 GMT` | Holds the date and time at which the message originated. It's preferred to convert the time to the standard [UTC](https://en.wikipedia.org/wiki/Coordinated_Universal_Time) time zone.                                                                                                                                                                                                    |
| `Connection` | `Connection: close`                   | Dictates if the current network connection should stay alive after the request finishes. Two commonly used values for this header are `close` and `keep-alive`. The `close` value from either the client or server means that they would like to terminate the connection, while the `keep-alive` header indicates that the connection should remain open to receive more data and input. |

#### Entity Headers
Similar to general headers, [Entity Headers](https://www.w3.org/Protocols/rfc2616/rfc2616-sec7.html) can be `common to both the request and response`. These headers are used to `describe the content` (entity) transferred by a message. They are usually found in responses and POST or PUT requests.

| **Header**         | **Example**                   | **Description**                                                                                                                                                                                                                                                            |
| ------------------ | ----------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `Content-Type`     | `Content-Type: text/html`     | Used to describe the type of resource being transferred. The value is automatically added by the browsers on the client-side and returned in the server response. The `charset` field denotes the encoding standard, such as [UTF-8](https://en.wikipedia.org/wiki/UTF-8). |
| `Media-Type`       | `Media-Type: application/pdf` | The `media-type` is similar to `Content-Type`, and describes the data being transferred. This header can play a crucial role in making the server interpret our input. The `charset` field may also be used with this header.                                              |
| `Boundary`         | `boundary="b4e4fbd93540"`     | Acts as a marker to separate content when there is more than one in the same message. For example, within a form data, this boundary gets used as `--b4e4fbd93540` to separate different parts of the form.                                                                |
| `Content-Length`   | `Content-Length: 385`         | Holds the size of the entity being passed. This header is necessary as the server uses it to read data from the message body, and is automatically generated by the browser and tools like cURL.                                                                           |
| `Content-Encoding` | `Content-Encoding: gzip`      | Data can undergo multiple transformations before being passed. For example, large amounts of data can be compressed to reduce the message size. The type of encoding being used should be specified using the `Content-Encoding` header.                                   |

#### Request Headers
The client sends [Request Headers](https://tools.ietf.org/html/rfc2616) in an HTTP transaction. These headers are `used in an HTTP request and do not relate to the content` of the message. The following headers are commonly seen in HTTP requests.

|**Header**|**Example**|**Description**|
|---|---|---|
|`Host`|`Host: www.inlanefreight.com`|Used to specify the host being queried for the resource. This can be a domain name or an IP address. HTTP servers can be configured to host different websites, which are revealed based on the hostname. This makes the host header an important enumeration target, as it can indicate the existence of other hosts on the target server.|
|`User-Agent`|`User-Agent: curl/7.77.0`|The `User-Agent` header is used to describe the client requesting resources. This header can reveal a lot about the client, such as the browser, its version, and the operating system.|
|`Referer`|`Referer: http://www.inlanefreight.com/`|Denotes where the current request is coming from. For example, clicking a link from Google search results would make `https://google.com` the referer. Trusting this header can be dangerous as it can be easily manipulated, leading to unintended consequences.|
|`Accept`|`Accept: */*`|The `Accept` header describes which media types the client can understand. It can contain multiple media types separated by commas. The `*/*` value signifies that all media types are accepted.|
|`Cookie`|`Cookie: PHPSESSID=b4e4fbd93540`|Contains cookie-value pairs in the format `name=value`. A [cookie](https://en.wikipedia.org/wiki/HTTP_cookie) is a piece of data stored on the client-side and on the server, which acts as an identifier. These are passed to the server per request, thus maintaining the client's access. Cookies can also serve other purposes, such as saving user preferences or session tracking. There can be multiple cookies in a single header separated by a semi-colon.|
|`Authorization`|`Authorization: BASIC cGFzc3dvcmQK`|Another method for the server to identify clients. After successful authentication, the server returns a token unique to the client. Unlike cookies, tokens are stored only on the client-side and retrieved by the server per request. There are multiple types of authentication types based on the webserver and application type used.|

A complete list of request headers and their usage can be found [here](https://tools.ietf.org/html/rfc7231#section-5).

#### Response Headers
[Response Headers](https://tools.ietf.org/html/rfc7231#section-7) can be `used in an HTTP response and do not relate to the content`. Certain response headers such as `Age`, `Location`, and `Server` are used to provide more context about the response. The following headers are commonly seen in HTTP responses.

|**Header**|**Example**|**Description**|
|---|---|---|
|`Server`|`Server: Apache/2.2.14 (Win32)`|Contains information about the HTTP server, which processed the request. It can be used to gain information about the server, such as its version, and enumerate it further.|
|`Set-Cookie`|`Set-Cookie: PHPSESSID=b4e4fbd93540`|Contains the cookies needed for client identification. Browsers parse the cookies and store them for future requests. This header follows the same format as the `Cookie` request header.|
|`WWW-Authenticate`|`WWW-Authenticate: BASIC realm="localhost"`|Notifies the client about the type of authentication required to access the requested resource.|

#### Security Headers
Finally, we have [Security Headers](https://owasp.org/www-project-secure-headers/). With the increase in the variety of browsers and web-based attacks, defining certain headers that enhanced security was necessary. HTTP Security headers are `a class of response headers used to specify certain rules and policies` to be followed by the browser while accessing the website.

|**Header**|**Example**|**Description**|
|---|---|---|
|`Content-Security-Policy`|`Content-Security-Policy: script-src 'self'`|Dictates the website's policy towards externally injected resources. This could be JavaScript code as well as script resources. This header instructs the browser to accept resources only from certain trusted domains, hence preventing attacks such as [Cross-site scripting (XSS)](https://en.wikipedia.org/wiki/Cross-site_scripting).|
|`Strict-Transport-Security`|`Strict-Transport-Security: max-age=31536000`|Prevents the browser from accessing the website over the plaintext HTTP protocol, and forces all communication to be carried over the secure HTTPS protocol. This prevents attackers from sniffing web traffic and accessing protected information such as passwords or other sensitive data.|
|`Referrer-Policy`|`Referrer-Policy: origin`|Dictates whether the browser should include the value specified via the `Referer` header or not. It can help in avoiding disclosing sensitive URLs and information while browsing the website.|

> [!note] 
> This section only mentions a small subset of commonly seen HTTP headers. There are many other contextual headers that can be used in HTTP communications. It's also possible for applications to define custom headers based on their requirements. A complete list of standard HTTP headers can be found [here](https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers).

#### cURL
The flag `-I` shows only the headers of the response(sends a `HEAD` request), to see both the headers and the body we use `-i` flag.
```shell-session ln:false
Skkippie@htb[/htb]$ curl -I https://www.inlanefreight.com

Host: www.inlanefreight.com
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_14_5) AppleWebKit/605.1.15 (KHTML, like Gecko)
Cookie: cookie1=298zf09hf012fh2; cookie2=u32t4o3tb3gg4
Accept: text/plain
Referer: https://www.inlanefreight.com/
Authorization: BASIC cGFzc3dvcmQK

Date: Sun, 06 Aug 2020 08:49:37 GMT
Connection: keep-alive
Content-Length: 26012
Content-Type: text/html; charset=ISO-8859-4
Content-Encoding: gzip
Server: Apache/2.2.14 (Win32)
Set-Cookie: name1=value1,name2=value2; Expires=Wed, 09 Jun 2021 10:18:14 GMT
WWW-Authenticate: BASIC realm="localhost"
Content-Security-Policy: script-src 'self'
Strict-Transport-Security: max-age=31536000
Referrer-Policy: origin
```

Also, we can send custom headers with curl, with the `-H` flag, but some headers have their own flags. For example `-A` is the flag for `User-Agent` , as follows.
```shell-session ln:false
Skkippie@htb[/htb]$ curl https://www.inlanefreight.com -A 'Mozilla/5.0'

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN">
<html><head>
...SNIP...
```

## 5.  HTTP Methods and Codes
HTTP supports multiple methods for accessing a resource. In the HTTP protocol, several request methods allow the browser to send information, forms, or files to the server. These methods are used, among other things, to tell the server how to process the request we send and how to reply.

#### Request Methods
The following are some of the commonly used methods:

|**Method**|**Description**|
|---|---|
|`GET`|Requests a specific resource. Additional data can be passed to the server via query strings in the URL (e.g. `?param=value`).|
|`POST`|Sends data to the server. It can handle multiple types of input, such as text, PDFs, and other forms of binary data. This data is appended in the request body present after the headers. The POST method is commonly used when sending information (e.g. forms/logins) or uploading data to a website, such as images or documents.|
|`HEAD`|Requests the headers that would be returned if a GET request was made to the server. It doesn't return the request body and is usually made to check the response length before downloading resources.|
|`PUT`|Creates new resources on the server. Allowing this method without proper controls can lead to uploading malicious resources.|
|`DELETE`|Deletes an existing resource on the webserver. If not properly secured, can lead to Denial of Service (DoS) by deleting critical files on the web server.|
|`OPTIONS`|Returns information about the server, such as the methods accepted by it.|
|`PATCH`|Applies partial modifications to the resource at the specified location.|

The list only highlights a few of the most commonly used HTTP methods. The availability of a particular method depends on the server as well as the application configuration. For a full list of HTTP methods, you can visit this [link](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods).

> [!note]  
> Most modern web applications mainly rely on the `GET` and `POST` methods. However, any web application that utilizes REST APIs also rely on `PUT` and `DELETE`, which are used to update and delete data on the API endpoint, respectively. Refer to the [Introduction to Web Applications](https://academy.hackthebox.com/module/details/75) module for more details.

#### Status Codes
HTTP status codes are used to tell the client the status of their request. An HTTP server can return five classes of status codes:

|**Class**|**Description**|
|---|---|
|`1xx`|Provides information and does not affect the processing of the request.|
|`2xx`|Returned when a request succeeds.|
|`3xx`|Returned when the server redirects the client.|
|`4xx`|Signifies improper requests `from the client`. For example, requesting a resource that doesn't exist or requesting a bad format.|
|`5xx`|Returned when there is some problem `with the HTTP server` itself.|

The following are some of the commonly seen examples from each of the above HTTP status code classes:

|**Code**|**Description**|
|---|---|
|`200 OK`|Returned on a successful request, and the response body usually contains the requested resource.|
|`302 Found`|Redirects the client to another URL. For example, redirecting the user to their dashboard after a successful login.|
|`400 Bad Request`|Returned on encountering malformed requests such as requests with missing line terminators.|
|`403 Forbidden`|Signifies that the client doesn't have appropriate access to the resource. It can also be returned when the server detects malicious input from the user.|
|`404 Not Found`|Returned when the client requests a resource that doesn't exist on the server.|
|`500 Internal Server Error`|Returned when the server cannot process the request.|

For a full list of standard HTTP status codes, you can visit this [link](https://developer.mozilla.org/en-US/docs/Web/HTTP/Status). Apart from the standard HTTP codes, various servers and providers such as [Cloudflare](https://support.cloudflare.com/hc/en-us/articles/115003014432-HTTP-Status-Codes) or [AWS](https://docs.aws.amazon.com/AmazonSimpleDB/latest/DeveloperGuide/APIError.html) implement their own codes.

## 6. GET
When we visit any URL, we send a GET request to obtain the content at that URL.
#### HTTP Basic Auth
When we visit the exercise found at the end of this section, it prompts us to enter a username and a password. Unlike the usual login forms, which utilize HTTP parameters to validate the user credentials (e.g. POST request), this type of authentication utilizes a `basic HTTP authentication`, which is handled directly by the webserver to protect a specific page/directory, without directly interacting with the web application.

>[!note] 
>The entire section talks about Basic Auth, it is authentication like this: `{sh icon}curl http://admin:admin@<url>` or `{sh icon} curl -u admin:admin <url>`

#### HTTP Authorization Header
The auth header can be seen like this:
````shell-session ln:false
> Authorization: Basic YWRtaW46YWRtaW4=
````

So, how we can see, the basic auth pass through the headers, using curl: 
`{sh icon} curl -H 'Authorization: Basic YWRtaW46YWRtaW4=' http://<SERVER_IP>:`

Get parameters are in the url with the `?` special character.

## 7. POST
Unlike HTTP `GET`, which places user parameters within the URL, HTTP `POST` places user parameters within the HTTP Request body. This has three main benefits:

- `Lack of Logging`: As POST requests may transfer large files (e.g. file upload), it would not be efficient for the server to log all uploaded files as part of the requested URL, as would be the case with a file uploaded through a GET request.
- `Less Encoding Requirements`: URLs are designed to be shared, which means they need to conform to characters that can be converted to letters. The POST request places data in the body which can accept binary data. The only characters that need to be encoded are those that are used to separate parameters.
- `More data can be sent`: The maximum URL Length varies between browsers (Chrome/Firefox/IE), web servers (IIS, Apache, nginx), Content Delivery Networks (Fastly, Cloudfront, Cloudflare), and even URL Shorteners (bit.ly, amzn.to). Generally speaking, a URL's lengths should be kept to below 2,000 characters, and so they cannot handle a lot of data.
#### cURL
To send a POST request using curl, we use `-X POST` flag and `-d` flag to sen data, for example:
`{sh icon} curl -X POST <url> -d '{"search":"flag"}'` 

>[!note] 
>Some pages redirects after a successful login, so we can use `-L` flag to follow this with curl

- To send cookies with curl we use the `-b` flag, for example:
`{sh icon} curl -X POST <url> -d '{"search":"flag"}' -b 'PHPSESSID=00svb42empk43t48kk76nloigj'` 

- Also we can use `-H` with the parameter `{sh}'Cookie: PHPSESSID=00svb42empk43t48kk76nloigj'`

- We send information to the server with `-d` flag, normally JSON data, you need to especify this in the header `Content-Type`
- A complete example: 
`{sh icon} curl -X POST http://94.237.122.241:43889/search.php -H 'Cookie: PHPSESSID=00svb42empk43t48kk76nloigj' -H 'Content-Type: application/json' -d '{"search":"flag"}'`

## 8. CRUD API
CRUD API expose endpoints for the client. The client send request to the server through the API.
#### CRUD
As we can see, we can easily specify the table and the row we want to perform an operation on through such APIs. Then we may utilize different HTTP methods to perform different operations on that row. In general, APIs perform 4 main operations on the requested database entity:

|Operation|HTTP Method|Description|
|---|---|---|
|`Create`|`POST`|Adds the specified data to the database table|
|`Read`|`GET`|Reads the specified entity from the database table|
|`Update`|`PUT`|Updates the data of the specified database table|
|`Delete`|`DELETE`|Removes the specified row from the database table|
# References
- [[Hack The Box]]
- [[HTB Module]]
