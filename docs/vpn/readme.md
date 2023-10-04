# How to setup Wireguard VPN server behind ASUS TUF AX3000 v2?
In this little guide I will present my solution to setup Raspberry PI 4 hosted VPN server, and its access through the ASUS router.
## Prerequisites
- Raspberry PI 4 - *PI version is up to your favour, no recommendations rised* - with fix IP address on the local LAN (*Or at least bound the device's MAC address to the fix IP address by the router - see documentation of the AX3000 for more info if needed!*).
- ASUS TUF AX3000 v2 wifi router - *firmware updated to the latest - check device's web site at ASUS home*

## Prepare Raspberry PI 4
Before setup the **pivpn** package on your Raspberry PI 4, it's advised to refresh the PI using ```apt update -y``` and ```apt upgrade -y``` - by the way the **pivpn** installation process will execute it as well.
Then - as you probably have done many times before - you can issue the following command ```curl -L https://install.pivpn.io | bash``` and follow the instructions on the terminal to install the VPN server - in this case the Wireguard VPN server - on the Raspberry PI 4.

### Hints:

-  At DHCP reservation window you should select fixed IP address - you need to setup this feature on your own Raspberry PI device. See the docs how to achieve this.

-  If there is no other user installed on your Raspberry PI, then stick with user 'pi'.

-  At installation mode windows - when you have to choose between OpenVPN or Wireguard VPN server installatio - you select the latter.

-  When installer asks for default port for Wireguard, <u>you shall pick another port numbber</u> than Wireguard's default **51820**!!!

-  Better to use router's DNS settings - see WAN settings on your ASUS TUF AX3000 v2 - which means (in my case) simply select your router's IP address as a DNS server.

-  When installer asks wether public IP address or domain name will be used when client connets to the VPN server - through the wifi router - you may select  domain name (if no fix public IP address is available, but you have a DDNS account somewhere...in my case I have registered on DynDNS.org, therefore I can use my domain name.) If you have not got fixed public IP address, better to have an account at one of the free or paid DDNS provider. Further more you would like to utilize your DDNS provider's ddclient utility to update the actual public IP address assigned by your ISP time to time. (*On Raspberry PI there is a package called ddclient to handle this issue.*)
-  Create client credentials using ```pivpn add``` command as desired.
-  Get newly created - or any of the existing - client's config by calling ```pivpn -qr <config_name>``` - where *<config_name>* is one of the created client's config on your Raspberry PI 4.
-  Add your client config to your device - where Wireguard client installed: e.g. IOS device or Android device etc. (*See the appropriate documentation about client setup.*)

## Setup port forwarding on ASUS router

After all at this point the VPN server should be up and running. Let's setup the port forwarding on the ASUS TUF AX3000 v2.
You need to login to the router's WEB GUI first. Then navigate to the **WAN** page where you can setup the port forwarding feature.

When you're on the **WAN** subpage, then you need to select the _curl -L https://install.pivpn.io | bashirtual Server / Port Forwarding_ tab to navigate the setup page.
There you should hit the &plus; sign. Then setup the port forwarding as you previously configured on Raspberry PI Wireguard VPN - apply the same port number in the source and destination port fields as you defined earlier during the Wireguard setup.

    Note! 
  **Do not use Wireguard's default port number!!!!**

