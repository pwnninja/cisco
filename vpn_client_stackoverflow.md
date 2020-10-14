Vendor: Cisco https://www.cisco.com

Product: Cisco Router RV110W and other router products

Tested Version: RV110W V1.2.1.7

Type: Stack overflow

Author: Shizhi He(Wuhan University)

I found a buffer overflow vulnerability in the router's web server--httpd. While processing the "vpn_account" parameter for a post request, the value is directly copied to to a variable on the stack using 'sscanf', which overrides the return address of the function. A remote attacker can leak information or hijack program control flow, leading to a RCE. 
The details are shown below:
![image](https://github.com/pwnninja/cisco/blob/main/images/vpn_clientStackoverflow1.PNG)
POC: 
![image](https://github.com/pwnninja/cisco/blob/main/images/vpn_clientStackoverflow3.PNG)

![image](https://github.com/pwnninja/cisco/blob/main/images/vpn_clientStackoverflow2.PNG)


As you can see in the above figure, if an attacker post data "vpn_account=x,x,x,x"(string x is very long), the return address of the function will be overriden and result in a DoS.
