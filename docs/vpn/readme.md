# How to setup Wireguard VPN server behind ASUS TUF AX3000 v2?
In this little guide I will present my solution to setup Raspberry PI 4 hosted VPN server, and its access through the ASUS router.
## Prerequisites
- Raspberry PI 4 - *PI version is up to your favour, no recommendations rised* - with fix IP address on the local LAN (*Or at least bound the device's MAC address to the fix IP address by the router - see documentation of the AX3000 for more info if needed!*).
- ASUS TUF AX3000 v2 wifi router - *firmware updated to the latest - check device's web site at ASUS home*

## Prepare Raspberry PI 4
Before setup the **pivpn** package on your Raspberry PI 4, it's advised to refresh the PI using ```apt update -y``` and ```apt upgrade -y``` - by the way the **pivpn** installation process will execute it as well.
Then - as you probably have done many times before - you can issue the following command ```curl -L https://install.pivpn.io | bash``` and follow the instructions on the terminal to install the VPN server - in this case the Wireguard VPN server - on the Raspberry PI 4.

    Hints:
      -  At DHCP reservation window you should select fixed IP address - you need to setup this feature on your own Raspberry PI device. See the docs how to achieve this.
      
        -  If there os no other user installed on your Raspberry PI, then stick with user '**pi**'
