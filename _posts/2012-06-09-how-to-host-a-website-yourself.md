---
layout: post
title: How to host a website yourself
tagline: Because why not?
category: [tutorials]
tags: [software, tutorial]
---
{% include JB/setup %}
As requested by one of my friends, this post will be a tutorial on how to host a small website on your local computer.

So you have a website you've made with HTML/JS/CSS and now you want it available online. The program that does this is called a web server. It's a program that runs as a service (usually) on your computer that watches a folder and makes the contents available via HTTP (a browser).

There are several webservers available and you could even write your own, but for the purpose of this tutorial I will be using the [Apache HTTP Server](http://httpd.apache.org/download.cgi). I may write a tutorial for Microsoft's IIS 7 in the future.

###Download and Install Apache
The first step is to [download](http://httpd.apache.org/download.cgi) it. If you're using Windows, I would suggest [this one](http://apache.mirrors.lucidnetworks.net//httpd/binaries/win32/httpd-2.2.22-win32-x86-no_ssl.msi).

During installation, click `Next` until you get to the Server Information form.

*  `Network Domain` - test.com
*  `Server Name` - www.test.com
*  `Admin Email Address` - test@test.com
                          
###Configuration                        
Now you have a choice if you want to run the program on `port 80 as a service` or on `port 8080 when started manually`.
If you just want to try this out for a day or two and that's it, select the port 8080 option. If you want to continuously use this, select the port 80 one.

__Note:__ You you can run the service and the manual version on any port you want. These will just be the default settings, it's easy to change later.

After selecting what you decided on, select `Next` then select `Custom` setup type, click `Next` again.

Make note of the `Install to` path as you will need to access this later. If you don't like where it's installing to, click `Change...` to fix it.
Click `Next` after noting where the Install to is at, then click `Install`, and finally, click `Finish`.


What now?

Your next choice depends what type of setup you chose:

*  `As a service on port 80` - Notice the task tray has a new icon with the apache logo. Simply leftclick this icon and mouseover `Apache2.2` to get access to Starting, Stopping, and Restarting the server. It should be started already and thus, the `Start` option will be greyed out. You can tell it's running because there is a green play arrow in the icon.
*  `Manual startup on port 8080` - Open an explorer window and navigate to where you installed apache to. This will likely be `C:\Program Files (x86)\Apache Software Foundation\Apache2.2`. Once in this folder, open the `bin` folder. Run httpd.exe. This will bring up the command prompt and may say _httpd.exe: could not reliably determine....using &lt;ip&gt; for ServerName_. This can be ignored for testing/experimenting. 
                            

The next step is to try it out!

Open a browser and navigate to http://127.0.0.1 if you ran it as a service, or http://127.0.0.1:8080 if you ran it manually. The service one doesn't require :80 at the end because by default that's what HTTP runs on and is what browsers expect. You can put the :80 on anyway if you want. 

If everything went successful you should see <h1>It Works!</h1>Where is this coming from? 

Navigate up a directory from the `bin` folder so you are back in `apache2.2`. Open the `htdocs` folder. If you open the index.html file that exists in this folder with a text editor, you'll see that it's exactly what you saw in the browser. Make any changes to this html file or even bring in an entire website, as long as everything is under the `htdocs` folder it will be accessible via a browser. Keep this in mind if you decide to make it available to the rest of the internet, don't keep private files here!

###Sharing
So everything is working and you want to show your friends. You paste them the link and they say it doesn't work, what's happening?

Well the 127.0.0.1 ip address is special, it refers to your loopback address, so it only works to communicate with your own machine. This worked because the browser and the server were on the same computer. In the case of your friend, they may not be running a webserver so when they visit that ip address, it just times out since nothing is listening on that port on their computer. 

For you to share your website publicly, you must meet a few conditions:

*  If you are running on port 80, your ISP must not block this port. A few ISPs may block this port unless you pay more since a lot of them assume you want a business plan if you're hosting a web server. Double check on your ISP's website or call them to verify. If you're worried it won't work, just try it. If it doesn't work just change the port that apache runs on which I go over later in the document.
*  Your ports must be forwarded. [PortForward.com](http://portforward.com/english/routers/port_forwarding/) has good tutorials for this. They have tutorials for almost every model and brand of router. Just select your router manufacturer, then model, then select Apache. Follow the instructions, it tells you to forward port 80 and 443 (default for HTTPS). You should put in the port number your apache is listening on. Fowarding 443 isn't necessary if you aren't going to use HTTPS.
*  Once that's done, all you need to do is obtain your public IP address. This can be done by going to [http://www.whatismyip.com/](http://www.whatismyip.com/) and it will tell you. Format your link as such: http://&lt;ip&gt;:&lt;portNumber&gt; for example if your ip is 1.2.3.4 and apache is listening on port 81, the url would be http://1.2.3.4:81
*  Your firewalls are properly configured to allow connections through port 80 or whatever port you're having apache run on.
  
###Apache Configuration
`apache2.2` - This refers to the folder where apache was installed to. This is probably _C:\Program Files (x86)\Apache Software Foundation\Apache2.2_
`httpd.conf` - apache2.2/conf/httpd.conf

#####How to change the port number.
Open up the `httpd.conf` file in a text editor such as [Notepad++](http://notepad-plus-plus.org/download/v6.1.3.html)
Around line 46 there will be a line that says

    Listen 80
or if your setup type is manual

    Listen 8080

Change the 80 or 8080 to any number you want between 1-65536. 
Save your changes to the file then restart apache. If you have the service installed this can be done by clicking on the icon. If you have the manual setup, just close the command prompt and run `httpd.exe` again.


###FAQ
__Q__: Do I have to port forward if I'm sharing the link with someone in my house?

__A__: Most likely not, if you are both connected to the same router, you should be able to give them your private IP address that was assigned by your router. You can check what this is by opening a command prompt and executing the command `ipconfig` and looking for the IPv4 Address on the correct adapter. It will probably be something like `192.168.1.X` as this is the form for most private IP addresses.