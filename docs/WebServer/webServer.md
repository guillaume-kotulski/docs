---
id: webServer
title: About 4D Web Server
---

4D in local mode, 4D in remote mode and 4D Server include a web server engine that enables you to publish 4D databases or any type of HTML page on the web. 

## Easy Publication

You can start or stop publication of the database on the web at any time. To do so, you just need to choose a menu command or execute a language command.

## Dedicated Database Methods

`On Web Authentication Database Method` and `On Web Connection Database Method` are the entry points of requests in the web server; they can be used to evaluate and route any type of request.

## Special Tags and URLs

The 4D Web Server offers numerous mechanisms that enable interaction with user actions, in particular:

*	[special tags](webServerSecurity.md#available-through-4d-tags-and-urls) can be included in web pages in order to initiate processing by the web server at the time when they are sent to browsers.

*	[special URLs](webServerMgmt.md#website-management-urls) that enable 4D to be called in order to execute any action.

*	these URLs can also be used as form actions to trigger processing when the user posts HTML forms.

## Manage Sessions

The 4D Web Server includes complete automatic features for easily managing [web sessions](webServerSessions.md) (user sessions) based on cookies.

## Access Security

Several automatic configuration options allow you to grant specific access authorizations to web browsers or to use the password system integrated into 4D. You can define a "[Generic Web User](webServerSecurity.md#generic-web-user)" to simplify access management within the database.

The `On Web Authentication Database Method` allows you to evaluate any request before it is processed by the web server. Moreover, the ability to define a [default HTML root](webServerSecurity.html#default-html-root) folder allows you to restrict access to files on disk.

Finally, you must designate individually the project methods that may be executed via the web.

## TLS Connections

Your 4D Web Server can communicate with browsers in secured mode through the [TLS protocol](webServerConnectSecurity.html#tls-protocol-https) (Transport Layer Security). This protocol, compatible with most web browsers, authenticates the sender and receiver and guaranties the confidentiality and integrity of the exchanged information.


## Extended Format Support 

### WML

4D Web Server supports WML (Wireless Markup Language) technology. This feature allows a mobile phone or a PDA’s owner to read and enter data in a 4D database.

The WML language associated to the WAP (Wireless Application Protocol) is developed by several companies. The WAP technology offers a set of network communication tools so that mobile phones and PDA users can visualize text published on web pages. The WML technology is open and free of charge. For more information on WML, please refer to the [Phone.com](http://www.phone.com/) website.

The data can be entered or read through WML pages using `4DTEXT` or `4DSCRIPT` tags.
	
Here is the list of the WML documents supported by 4D Web Server:<p>

|Extension|	MIME Type|	Description|
|---|---|---|
|.wml|	text/vnd.wap.wml|	WML pages (always supported by 4D*)|
|.wmls|	text/vnd.wap.wmlscript	|WML Scripts (on the client’s side)|
|.wmlc|	application/vnd.wap.wmlc|	WML binary pages|
|.wmlsc|	application/vnd.wap.wmlscript|	WML binary scripts|
|.wbmp|	picture/vnd.wap.wbmp|	Bitmap images for mobile phones (not always supported)|

\* Allows dynamic data insertion through `4DTEXT` and `4DSCRIPT` type tags.

### XML

The 4D Web Server supports .xml, .xls, and .dtd documents which are sent with the “text/xml” and “text/xsl” MIME types.

4D analyzes their content and processes their `4DTEXT` or `4DSCRIPT` type tags (if any) in order to generate dynamic XML.<p>

### GZIP Compression
	
The 4D Web Server also extends the support of gzip compression: 

*	after a "negotiation" between the web server and client, all exchanges can potentially be compressed, for an immediate performance boost.

## Simultaneous Database Operations 

### 4D in local mode and the web

If you publish a 4D database on the web using 4D in local mode, you can simultaneously:
*	Use the database locally with 4D
*	Connect to the database using web browsers

### 4D Server and the web

If you publish a 4D database on the web using 4D Server, you can simultaneously connect to and operate the 4D database, using:
*	4D remote workstations
*	Web browsers

### 4D in remote mode and the web

When a 4D database is published on the web with 4D client, it is possible to connect to the 4D database and to simultaneously use it:
*	via 4D remote machines
*	via web browsers - In this case, if the database is also published with 4D Server, the web browsers can connect to the published database via a 4D client machine or via 4D Server. Moreover, this allows different data access modes to be handled (public, administration, etc.).<p>The basic mechanisms of the 4D Web Server are used in a similar manner by 4D in remote mode. The operation of language commands is usually identical, whether the command be executed on 4D in local mode, 4D Server or 4D in remote mode. The main point is that commands are applied to the website of the machine on which they are executed. You must manage this using the `Execute on server` / `EXECUTE ON CLIENT` commands.


## Client Load Balancing 

Since any 4D machine in remote mode can be used as a web server, you can set up a dynamic web server system with a load balancer. This offers extensive development possibilities, including, more particularly:

*	the setting-up of a load-balancing system in order to optimize the performance of the 4D Web server: using a mirror of the website that is installed on each 4D Web server, a load balancer (hardware or software) will send requests to the client machines on the basis of their current load.<p>![](assets/en/WebServer/loadBalance.png)

*	the setting-up of a fault tolerance Web server: the 4D website is mirrored on two or more 4D client machines. If one 4D Web server fails, another one takes over.

*	the creation of different views of the same data, for instance depending on the origin of the requests. Within a company network, a web server on a protected 4D client machine can serve Intranet requests and a web server on another 4D client machine, located beyond the firewall, will serve Internet requests.

*	the distribution of tasks between web servers on different 4D client machines: one 4D Web server can be in charge of SOAP requests, another can handle standard requests, and so on.

## Custom HTTP Error Pages  

The 4D Web Server allows you to customize HTTP error pages sent to clients, based on the status code of the server response. Error pages refer to:

*	status codes starting with 4 (client errors), for example 404

*	status codes starting with 5 (server errors), for example 501. 

For a full description of HTTP error status codes, you can refer to the [List of HTTP status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) (Wikipedia).

#### How does it work?  

To replace default 4D Web Server error pages with your own pages you just need to:

*	put custom HTML pages at the first level of the application's web folder,

*	name the custom pages "{statusCode}.html" (for example, "404.html"). 

You can define one error page per status code and/or a generic error page for a range of errors, named "{number}xx.html". For example, you can create "4xx.html" for generic client errors. The 4D Web Server will first look for a {statusCode}.html page then, if it does not exist, a generic page.

For example, when an HTTP response returns a status code 404:

1.	4D Web Server tries to send a "404.html" page located in the application's web folder.

2.	If it is not found, 4D Web Server tries to send a "4xx.html" page located in the application's web folder.

3.	If not found, 4D Web Server then uses its default error page.

#### Example  

If you define the following custom pages in your web folder:

![](assets/en/WebServer/errorPage.png)

*	the "403.html" or "404.html" pages will be served when 403 or 404 HTTP responses are returned respectively,

*	the "4xx.html" page will be served for any other 4xx error status (400, 401, etc.),

*	the "5xx.html" page will be served for any 5xx error status.



