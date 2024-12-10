# Unraid-Stun-Turn-Server
Unraid Stun-Turn-Server With NextCloud Talk Instructions 

This assumes that you already have a working nextcloud installation with correctly working reverse proxy. 

1.	Install and configure the Stun-Turn-Server Docker Container

&ensp; a.	Install Stun-Turn-Server from community applications

&ensp;b.	It is suggested to use a custom IP address for this docker container. This will make port forwarding easier and you don’t have to worry about conflicting IP addresses and ports.  

&ensp;c.	Read through the different options when installing, but you will need to change the following.

&ensp;&ensp;i.	Static Secret – follow the instructions as listed. Keep this value as it will need to be used later in the nextcloud instance. 

&ensp;&ensp;ii.	Realm – In most cases this should be the same as your reverse domain name for you nextcloud instance that points to your public IP. In my example it is: turn:nextcloud.yourdomain.com

&ensp;&ensp;iii.	Certificate Generation – Country – Put in your two character country code. For United States it will be: US

&ensp;&ensp;iv.	Certificate Generation – State or Providence– Put in your state or providence

&ensp;&ensp;v.	Certificate Generation – Locality – A more specific location than state or Providence

&ensp;&ensp;vi.	Certificate Generation – Origination – What the nextcloud instance is called

&ensp;d.	Those should be all of the required values. Apply the config and allow the docker to pull down

2.	Port forward UDP and TCP port 5349 from your firewall to the custom IP used for the Stun Turn server. It is suggested to use this port but it can be changed if needed. The exact steps to port forward depend on your network configuration and firewall. I won’t cover the specific steps for this.

3.	Test the server is working correctly

&ensp;a.	Visit the website below to test the server: https://webrtc.github.io/samples/src/content/peerconnection/trickle-ice/ 

&ensp;b.	Click on the default stun server and remove it. 

&ensp;c.	In the STUN or TURN URI input the following values individually then click add server. Note for my instance I’m using the default stun server. I was not able to get the installed server stun option to work.

&ensp;&ensp;i.	stun: stun.nextcloud.com:443

&ensp;&ensp;ii.	turn:nextcloud.yourdomain.com:5349

&ensp;d.	Scroll down to ICE options, and use all IceTransport Values

&ensp;e.	Click gather candidates

&ensp;f.	If successful you should see multiple hosts listed for UDP and TCP as well as your public IP address as srflx type. The hosts indicate a working turn server and srflx with IP address indicates a working stun server. 
4.	Nextcloud Integration

&ensp;a.	Login to your nextcloud account as admin. 

&ensp;b.	Go to admin > administration settings > Under administration go to talk

&ensp;c.	Scroll down to STUN and TURN server settings

&ensp;d.	For Stun I’m using the default: stun.nextcloud.com:443

&ensp;e.	For TURN fill out the fields as follows:

&ensp;&ensp;i.	Turn and Turns:

&ensp;&ensp;ii.	Turn server URL: 

&ensp;&ensp;&ensp;1.	nextcloud.yourdomain.com:5349

&ensp;&ensp;iii.	Turn Server Secret:

&ensp;&ensp;&ensp;1.	The value from step one that was generated with a terminal command.

&ensp;&ensp;iv.	UDP and TCP

&ensp;f.	NOTE: During my setup I was not able to get a successful test using the button next to the UPD and TCP selection. There may be a bug with how it operates. I was able to verify correct operation through various tests. 
