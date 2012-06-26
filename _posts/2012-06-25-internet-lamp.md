---
layout: post
title: "Internet Lamp"
tagline: ""
category: [statuses]
tags: [status, hardware, software]
---
{% include JB/setup %}
>Just because it doesn't have an ethernet port doesn't mean you can't control it over the Internet

I have successfully controlled a lamp via the Internet. While I'm sure there are much less convoluted ways, this post will give a brief overview of how I did it.
This isn't meant to be a tutorial, it's more of a high level summary. Here is a short video of it in action:
<iframe width="480" height="360" src="http://www.youtube.com/embed/x9v0fwARCi0" frameborder="0" allowfullscreen></iframe>

###Items Used:

* [X10 Wireless Transceiver Module](http://www.x10.com/automation/x10_tm751.htm)
* [X10 Appliance Module](http://www.x10.com/promotions/am466_cat_hm.html)*
* [X10 Firecracker](http://www.x10.com/products/firecracker_x10_cm17a_br1ab.htm)
* A lamp

*This may not be necessary. Some X10 Wireless Transceiver Modules have an Appliance Module built-in. The one I have claims that it does but I couldn't get it work.

###Software Used:

* [cm17a](https://bitbucket.org/davcamer/ccnet/src/0f34cb2e1ffb/tools/cm17a/)
* [PubNub](http://www.pubnub.com/)

###My Scripts:  
**Python 'server':**  

{% highlight python %}
import os
from Pubnub import Pubnub

pubnub = Pubnub("pub-enter-your-key-here-thanks", "sub-enter-your-key-here-thanks", None, False)
def receive(message):
	print message
	if (message == "on"):
		print "turning A2ON"
		os.system("cm17a.exe 3 A2ON")
	elif (message == "off"):
		print "turning A2OFF"
		os.system("cm17a.exe 3 A2OFF")
	return True
	
def main():
	channel = "remote_lamp"
	print "Listening for messages on %s" % channel
	pubnub.subscribe({
		"channel" : channel,
		"callback": receive
	})

if __name__ == "__main__":
	main()
{% endhighlight python %}

**JavaScript UI**  

{% highlight html %}
<!DOCTYPE html>
<html lang="en">
<head>
<title>Lamp Remote</title>
</head>
<body>
	<div class="container">
		<button id="lamp-on">Lamp On</button>
		<button id="lamp-off">Lamp Off</button>
	</div>
<div pub-key="pub-enter-your-key-here-thanks" sub-key="sub-enter-your-key-here-thanks" ssl="off" origin="pubsub.pubnub.com" id="pubnub"></div>
<script src="http://cdn.pubnub.com/pubnub-3.1.min.js"></script>
<script type="text/javascript">
function lampOn() {
console.log('lamp on');
	PUBNUB.publish({
		channel  : "remote_lamp",
		message  : "on",
		callback : function(info) {
			console.log(info);
		}
	});
}
function lampOff() {
console.log('lamp off');
	PUBNUB.publish({
		channel  : "remote_lamp",
		message  : "off",
		callback : function(info) {
			console.log(info);
		}
	});
}
PUBNUB.bind(
    'click',
    PUBNUB.$('lamp-on'),
    function(element) {
		lampOn()
    }
);
PUBNUB.bind(
    'click',
    PUBNUB.$('lamp-off'),
    function(element) {
		lampOff()
    }
);
</script>
</body>
</html>
</html>
{% endhighlight html %}

I'm sure there are much more elegant ways of writing both of those scripts but I'm new to JavaScript and I put all of this together in under an hour (hooray libraries!).

###Explanation
1. Buttons are shown on a webpage.
2. JavaScript gets executed when the buttons are clicked, sending a message through the PubNub network.
3. The Python script receives these messages as it is subscribed to the channel the javascript is publishing messages to.
4. The python script decides which button was pressed based on the message and calls the cm17a.exe program with the correct arguments.
5. The cm17a.exe program sends the commands to the Firecracker
6. The Firecracker wirelessly transmits the commands to the Wireless Transceiver Module
7. The Wireless Transceiver Module relays the commands through the power lines in my house to the Appliance Module
8. Finally, the appliance module receives the command and turns the lamp on or off.

Now you can see why there is such a delay between clicking the buttons on the webpage and the lamp actually doing it :)
