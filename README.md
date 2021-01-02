### RaspberryPI 4 as Firewall

---------


**RaspberryPI 4 Model B as Firewall (Smoothwall Express 3.1)**


**FAQ:**

    Q: Why I choose Smoothwall Express 3.1

	A: I was looking to get Ipfire on my new Raspberry Pi but at the moment (30.12.2020) is Ipfire not supporting the RaspberryPi 4. The only Firewall that's running well on RaspberryPi is Smoothwall Express 3.1 . And yes its quite better that I was thinking! It has a lot of features and community driven mods. And for RaspberryPi are not so much Firewall DISTROS and especially for the Raspberry 4, Smoothwall Express 3.1 was the only one that I found. And the last update for SWE 3.1 was at Jul 14, 2020. 
	----------------------------------------------------------
	Q: It's only working on RaspberryPi 4?

	A: I don't test it, but I think yes. If someone try it on a RaspberryPi 3 Model B+, just send me a message on Twitter.
	----------------------------------------------------------
	Q: What should I learn?
	
	A: Definitly iptables. 
	https://en.wikibooks.org/wiki/Communication_Networks/IP_Tables
	----------------------------------------------------------
	Q: I can't use DHCP simultantly on PURPLE(Wi-Fi) and Green(Switch)
	
	A: It only works if PURPLE is in other subnet as GREEN.
	
	----------------------------------------------------------
	Q: Do I need all of your Equipment?
	
	A: If you have something like the Products that I named it shouldn't be a problem but what i definitely recommend you to buy is the "Aluminium heat sink with fan", because the Raspi will get hot.
	If you don't have it, then buy all of these things because you will need it all (except the DSL Router/Modem, i mean you should have one lol).
	----------------------------------------------------------
	Q: I can't access from PURPLE stuffs on GREEN like Webservices etc, what can i do?
	
	A: You need to allow tcp/udp on every port from PURPLE to GREEN and from GREEN to PURPLE. You can do this only for one device or for all devices. You can do this on cli with iptables or on the Webinterface under Networking-Internal.
	----------------------------------------------------------

	Q: I want to build my own iptables chains/rules and delete the one that get coocked up at booting...
	
	A: You can write a script and add it at the last line of /etc/rc.d/rc.sysinit or you can write/delete the standard one in /etc/rc.d/rc.firewall.up
	
	Your bestfriend is /etc/rc.d !!!!
	----------------------------------------------------------

	Q: I can't access the firewall from PURPLE, even https or ssh
	
	A: You need to allow it. You can allow it from the webinterface under services->remote access
	----------------------------------------------------------

	Q: It's PPPOE working?
	
	A: Yes, im using it as PPPOE with a FritzBox (Yes, you can use the fritzbox as modem https://deer-it.de/fritzbox-7412-modem-bridge-mode-pppoe-passthrough/).
	You can change the RED interface from the Webinterface to PPPOE. 
	----------------------------------------------------------

	A: Ports?
	
	Q: 222 - ssh , 441 - https 
	----------------------------------------------------------


**The equipment that i used:**

| Product  | Link  |
|:----------|:----------|
| USB 3.0 RJ45 10/100/1000 Gigabit Ethernet Adapter  | [https://amzn.to/3puxu9Z](https://amzn.to/3puxu9Z)   |
|  Aluminum heat sink with fan for Raspberry Pi 4B    | [https://amzn.to/3mZF4aM](https://amzn.to/3mZF4aM) |
 Raspberry Pi 4 Model B 4GB RAM    | [https://amzn.to/37UZrBU](https://amzn.to/37UZrBU) |
 MicroSD 64GB    | [https://amzn.to/3o09f2W](https://amzn.to/3o09f2W) |
 MicroSD USB Reader    | [https://amzn.to/34S6rh1](https://amzn.to/34S6rh1)|
 TP-Link TL-SG105 5-Ports Gigabit Network Switch   | [https://amzn.to/3aXZmiR](https://amzn.to/3aXZmiR) |
 3x LAN Kabel (use Gigabit Ethernet Cables), for example these from the link | [https://amzn.to/37TTuoK](https://amzn.to/37TTuoK)|
 MicroHDMI to HDMI Adapter | [https://amzn.to/38PFADn](https://amzn.to/38PFADn)
 And a DSL Router of course(i think you should have one lol) ||


**Download**

| Name  | Description  | Link
|:----------|:----------|:----------|
| RaspberryPi Imager  | We will need it to erase & format the MicroSD  |  [https://www.raspberrypi.org/software/](https://www.raspberrypi.org/software/)
Smoothwall patched for RaspberryPi 4 with update 11| The Smoothwall Open Source Project was set up in 2000 to develop and maintain Smoothwall Express - a Free firewall that includes its own security-hardened GNU/Linux operating system and an easy-to-use web interface, you can read more at [https://smoothwall.org](https://smoothwall.org)| [http://agcl.us/shortie/Express-3.1-SP5-pi4-64.zip](http://agcl.us/shortie/Express-3.1-SP5-pi4-64.zip) or from Mirror(hosted by me) [http://teodorcucu.net/downloads/Express-3.zip](http://teodorcucu.net/downloads/Express-3.zip)|

**Credits**

[https://community.smoothwall.org/forum/viewtopic.php?f=123&p=353493#p353493](https://community.smoothwall.org/forum/viewtopic.php?f=123&p=353493#p353493)


----

Part 1:
1. Open RaspberryPi Imager and choose Operating System
![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild0.png)

2. Scroll down and choose Erase
![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild1.png)

3. Select your SD Card
![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild2.png)
![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild3.png)

4. Click on Write
![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild4.png)
5. Now copy all the files from Express-3 to the SD Card
 ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild5-1.png)‚

Before booting:

- Insert the SD Card in your RaspberryPi. 
- Connect it to a monitor and you will need as well a keyboard. 

- The first ethernet cable with the usb-to-lan adapter and then to the router
- The second ethernet cable with the onboard lan to the switch
- The third one from the switch to your pc


Now we can start it.


Part 2.1:

1. Press Return 
![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild5.jpg)
2. Type 1 and press Return (we rename wlan0 to eth2 so keep in mind, eth2 is our WiFi interface) ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild6.jpg)
3. Press Return ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild7.jpg)
4. Press Return ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild8.jpg)
5. Press Return ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild9.jpg)
6. Press Return ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild10.jpg)
7. Press Return ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild11.jpg)
8. Chose your Country Code and press Return ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild12.jpg)
9. Now type 'yes' and press Return ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild13.jpg)
10. Select NO ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild14.jpg)
11. Select your Keyboard Mapping ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild15.jpg)
12. Select your Timezone ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild16.jpg)
13. If you want, you can change the hostname of our firewall to something else, if not press Return B![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild17.jpg)
14. Select Half-Open ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild18.jpg)

Part 2.2

**IMPORTANT**
:
We will use our USBtoEthernet-Adapter as RED Interface (for getting a working internet connection), the Onboard LAN as GREEN for the LAN and the Onboard WiFi as Purple



1. Choose Network Configuration Type ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild19.jpg)
2. Scroll down and select GREEN + PURPLE + RED ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild20.jpg)
3. Now choose Card Assignments ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild21.jpg)
4. Choose Ok and hit Return ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild22.jpg)
5. The USBtoEthernet Adapter as RED ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild23.jpg)
6. The Onboard Ethernet as GREEN ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild24.jpg)
7. The Onboard WiFi as Purple ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild25.jpg)
8. Now we choose Adress Settings ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild26.jpg)
9. Choose Green ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild27.jpg)
10. Press Return ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild28.jpg)
11. We will choose the standard one 192.168.0.1/24 ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild29.jpg)
12. Now we Choose Purple ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild27.jpg)
13. For purple we use 192.168.1.1 and /24 Mask (you can do later the routing etc) ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild30.jpg)
14. Now we select RED ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild31.jpg)
15. ATM we will use it as behind the router(not PPPOE, you can do this later) so we choose DHCP B![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild32.jpg)
16. Choose Done an hit return ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild33.jpg)
17. Choose DNS Settings ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild34.jpg)
18. Delete the 1.1.1.1 DNS Server (we will use the default one from RED, Router DNS)![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild35.jpg)
19. Choose DONE and hit return ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild34.jpg)
20. We choose DHCP Server Configuration ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild36.jpg)
21. We activate the DHCP Server Configuration for GREEN(make sure that you connect GREEN to Switch and a Ethernet Cable from Switch to your PC) ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild37.jpg)
22. Select FINISHED ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild38.jpg)
23. Choose a password for the user 'admin' (webinterface) ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild39.jpg)
24. Choose a password for the user 'root' (ssh) B![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild40.jpg)
25. We done, hit Return ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild41.jpg)


Part 3.0:

FIXING WIFI:

For some reason is the wifi broken... so we need to resolve that.

1. SSH on smoothwall / on port 222 (Port 222 is the standard port for ssh on Smoothwall) 17. Choose DNS Settings ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild42.png)
2. Now we will use my script for fix WIFI ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild43.png)

	
		bash <(wget -qO- https://raw.githubusercontent.com/teodorcucu/raspi4-smoothwall-wifi-fix/main/fix-wifi.sh)
	(Note that the Country Language is set to DE so you will need to change it after rebooting at /etc/hostapd/hostapd.purple.conf and reboot again.

3. Now we need activate DHCP for Purple WiFi, for that access the Webinterface and go to Services-dhcpd, scroll down to interface and choose Purple ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild44.png) ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild45.png)
4. Enable DHCP and set it up like in the picture ![ ](https://teodorcucu.net/assets/img/rpi-firewall-bilder/Bild46.png)

Thats it, now you can connect to the SSID 'Purple-Wifi' with the password 'password'. You can change it at /etc/hostapd/hostapd.purple.conf

