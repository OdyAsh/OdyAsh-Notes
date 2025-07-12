
Main sources:
* s1: https://www.totlpower.com/guide-to-choosing-the-right-usb-c-to-usb-c-cable/
	* Guide to Choosing the Right USB-C to USB-C Cable
* s2: https://www.youtube.com/watch?v=X5qCujdQeIg
	* "How to Read Phone Charger Voltage Specs" - Ask Leo!
	* This video and this content creator takes the OdyAsh Recommendation Stamp ™️®️©️!
* s3: https://www.youtube.com/watch?v=ajVwqpUnezA
	* "You're Probably Using the WRONG USB Charging Cable" - ThioJoe
* s4: https://www.youtube.com/watch?v=cqR_bwJi_e4
	* USB Power Explained (USB Power for Dummies!) - DPReview TV
* s5: https://learn.adafruit.com/understanding-usb-type-c-cable-types-pitfalls-and-more/cable-types-and-differences
	* Understanding USB Type C: Cable Types, Pitfalls and More
* s6: https://www.xda-developers.com/usb-standards-explained/
	* Everything you need to know about USB standards, speeds, and port types


# Charging vs Data Transfer Aspect

When talking about cables (specifically, their USB standards / port types), we care about one of two aspects (s1):
* Charging
	* Here, you'll see jargon like:
		* "3A", "5V", "15W", "PD", etc. for calculations.
	* This is what we're focusing on for the rest of these notes.
	* Side note 1 (completely optional): You can check [this](https://www.youtube.com/watch?v=1nx_n-wEtII) video to see how charging works; from A to Z :].
	* Side note 2: We rarely talk about Thunderbolt and other specific/proprietary charging types here, but you can check [this](https://www.youtube.com/watch?v=hScecDuwXLg) video which glosses over them. 
* Data transfer
	* Here, you'll see jargon like:
		* "480Mbps", "5Gbps", etc. for calculations.
* Confusingly though, you'll see these terminologies in both aspects:
	* "USB-A/B/Micro-B/C/etc." , "USB 1.0/2.0/3.0/etc." for USB types/versions in a cable.
	* "PD, thunderbolt, etc." mentioned in cables/devices/chargers.

So for now, let's focus on the charging aspect...

# 3 Aspects of Charging

When charging, there are 3 aspects to consider:
* the charger type.
* the device that needs to be charged.
* The cable that connects them.


# How to Read Phone Charger Voltage Specs and Multi Power Output Levels

TL;DR: If you understand the video in (s2), then:
* You'll know which charger (i.e., power source, i.e., power brick) to use for your phone
* You'll know if a charger supports multiple levels of power output or not.
* You'll have a [mental model](https://agileapplied.com/2017/11/18/mental-models/#:~:text=What%20business%20rules,The%20reason) of this sentence: "a device can be "smart" and hence tell the charger what power output level it requires". 
	* However, this "required output level" may not be delivered due to a third aspect that (s2) doesn't talk about: the charging cable.
	* Therefore, most of these notes discuss USB/ports of these charging cables, so that you know which charging cable to buy :].


# PD - Power Delivery

A quick detour: what's "PD"?:
* Previous USB power standards are limited in that they cannot provide multiple power levels for different devices. The USB PD specification, however, allows the power supply and device to negotiate for an optimum power delivery method ([source](https://www.allaboutcircuits.com/industry-articles/usb-pd-vs-usb-c-differences-benefits-and-adapters/#:~:text=Previous%20USB%20power%20standards%20are%20limited%20in%20that%20they%20cannot%20provide%20multiple%20power%20levels%20for%20different%20devices.%20The%20USB%20PD%20specification%2C%20however%2C%20allows%20the%20power%20supply%20and%20device%20to%20negotiate%20for%20an%20optimum%20power%20delivery%20method.)). Details ([source](https://electronics.stackexchange.com/a/450554)): 
	* The USB-PD standard allows for multiple output voltages on USB-C devices, 
	* but every USB-C power supply must initially output 5V and communicate with the device on the other end. 
	* If the other device does not specifically ask the power supply to output more than 5V it will just continue to put out 5V and no more .
	* Details: an article called [The Basics of USB Power Delivery Negotiations](https://acroname.com/blog/basics-usb-power-delivery-negotiations).
* Regarding devices: If you see ["PD" symbol](https://www.club-3d.com/en/technology/15/usb_c_over_alt_mode/#:~:text=support%20DisplayPort%20alt-,mode.,USB,-C%20port%20Apple) on a port of a device (e.g., a laptop), then that port will take a ***high wattage input*** to power it. 
	* In turn, that means that items connected to other ports on the device will get power if they need it, like phones, USB monitors and similar ([source](https://www.reddit.com/r/MiniPCs/comments/18934ow/comment/kboryzi/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)).
* Regarding chargers: See (s4, [6:45](https://youtu.be/cqR_bwJi_e4?t=406)) to check if it supports PD. TL;DR: PD chargers support multiple output levels.
* Regarding cables:
	* If a cable has < 60W max output power, then it is a non-PD cable ([source](https://www.reddit.com/r/anker/comments/m4xwyj/comment/gqx3c2b/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)).
	* PD cables start from 60W and upwards.


# Regarding Cables

Now, moving on to cables:

Here's a matrix illustrating the supported power guaranteed by each cable type:
* (E.g. of how to read the table: "ANY c-to-c cable is guaranteed to support up to 60W")

![](Attachments%20-%20USB%20Standards%20and%20Port%20Types%20of%20Charging%20Cables/Pasted%20image%2020250414102426.png)

(s3, [4:15](https://youtu.be/ajVwqpUnezA?t=255))

Side note1: A "C-to-A" cable can be named as an "A-to-C" cable (i.e., order doesn't matter).

Side note 2 (related to history): the "A" part of any cable has a history of supporting lower values. Details (s4, [2:22](https://youtu.be/cqR_bwJi_e4?t=141)):

![](Attachments%20-%20USB%20Standards%20and%20Port%20Types%20of%20Charging%20Cables/Pasted%20image%2020250414110756.png)

Therefore, I guess the "A" part of any C-to-A cable MUST be of type 3.2 :] 
* (since it's previously mentioned that C-to-A cables must support 15W).
* Proof (s4, [4:14](https://youtu.be/cqR_bwJi_e4?t=254)): "when USB C originally came out, it was the same as USB 3.2".

Now, moving on, see the "USB Power Delivery" (USB-PD) options above? there are technically 4 options for USB-PD ratings (not 3 as seen above):

![](Attachments%20-%20USB%20Standards%20and%20Port%20Types%20of%20Charging%20Cables/Pasted%20image%2020250414103022.png)

To rephrase (from what I understand), the [USB-IF](https://www.wikiwand.com/en/articles/USB_Implementers_Forum) has rated power delivery options into the above 4 options.
* Note: we're currently talking about the options of a power source.
	* E.g., [a phone charger](https://www.etechnog.com/2018/10/meaning-of-symbols-and-rating-of-mobile.html). 

However, cables are only capable (or caple-able, hehe) of handling 3 levels:

![](Attachments%20-%20USB%20Standards%20and%20Port%20Types%20of%20Charging%20Cables/Pasted%20image%2020250414102811.png)


Well then, how to tell if a C-to-C cable is 60W, 100W, or 240W? (s3, [6:35](https://youtu.be/ajVwqpUnezA?t=393)):
* 60W is the default.
	* I.e., most (old/basic) C-to-C cables are assumed to be 60W (i.e., 3A x 20V)
	* Therefore, they don't have an E-marker. Details: (s3, [10:10](https://youtu.be/ajVwqpUnezA?t=610))
* 100W/240W
	* Must have E-markers
	* There's no way to properly identify if it's 100 or 240 though.
	* So just get a 240W, as the former is deprecated (s3, [6:20](https://youtu.be/ajVwqpUnezA?t=381))


# How to Know Which Cable to Get Based on The Charger

Ok, but how to know which cable to get based on the charger?: Let's take a complicated example from (s2, [6:18](https://youtu.be/X5qCujdQeIg?t=378)):

If you have a charger called:

> 2025 Latest USB C Fast Charger,165W GaN 4-Port Charging Station Hub Block Cube, USB C Wall Charger Blocks with Dual Type C Ports, for iPad/iPhone 16 15 14 13 12 Pro Max Pixel Note Galaxy

which looks like this:

![](Attachments%20-%20USB%20Standards%20and%20Port%20Types%20of%20Charging%20Cables/Pasted%20image%2020250414174216.png)

Specifically:

![](Attachments%20-%20USB%20Standards%20and%20Port%20Types%20of%20Charging%20Cables/Pasted%20image%2020250414174319.png)

Then inspect its label:


![](Attachments%20-%20USB%20Standards%20and%20Port%20Types%20of%20Charging%20Cables/Pasted%20image%2020250414115209.png)

We see that the max option for USB-C is 20V-5A; this is calculated to 100W (which is the advertised maximum).

Same thing with USB-A (20V-1.5A --> 30W max)

And so, when this charger is connected to a device, a power delivery negotiation (mentioned in the notes above) is done to decide which output level is chosen for the device.

Notes: 
* Apparently, it's totally safe to use a higher rated charger (or cable) with a lower rated device ([source](https://youtu.be/nNWVwvAtY1Y?t=120)).
* I.e., current is drawn from your device, not pushed from the charger; You can always connect a charger that has a higher output to your device and your device will only pull what it requires/is designed to draw. 
	* Meaning that if you have a laptop that requests 65W, and you've got a charger that outputs a max of 100W, your laptop will only request 65W from the charger and the charger will be running at 65% vs buying a 65W charger that is running at 100% when charging your laptop ([source](https://www.reddit.com/r/ZephyrusG14/comments/md0e5c/comment/gs6l0zv/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button)).



# Details About Data Transfer Aspects of USB C

Extra details for USB C, but regarding the data transfer aspect, NOT the charging aspect:

![](Attachments%20-%20USB%20Standards%20and%20Port%20Types%20of%20Charging%20Cables/Pasted%20image%2020250414174654.png)

([s5](https://learn.adafruit.com/understanding-usb-type-c-cable-types-pitfalls-and-more/cable-types-and-differences))

If you run across the term “Full-featured” this a reference to speed and typically means [USB 3.1 Gen 2](https://www.transcend-info.com/Support/FAQ-1285).


"[Going forward](https://www.pcworld.com/article/2572128/an-updated-usb-logo-will-now-mark-the-fastest-docking-stations.html), the USB-IF, as of 2025, recommends labeling ports and cables by their speed, rather than the standard they support:" ([s5](https://learn.adafruit.com/understanding-usb-type-c-cable-types-pitfalls-and-more/cable-types-and-differences#:~:text=Going%20forward%2C%20the%20USB%2DIF%2C%20as%20of%202025%2C%20recommends%20labeling%20ports%20and%20cables%20by%20their%20speed%2C%20rather%20than%20the%20standard%20they%20support%3A))

![](Attachments%20-%20USB%20Standards%20and%20Port%20Types%20of%20Charging%20Cables/Pasted%20image%2020250414175227.png)

# Details About Different USB Types

![](Attachments%20-%20USB%20Standards%20and%20Port%20Types%20of%20Charging%20Cables/Pasted%20image%2020250414175341.png)

([s6](https://www.xda-developers.com/usb-standards-explained/#:~:text=costs.,USB))