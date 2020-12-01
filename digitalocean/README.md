# How to Configure a Droplet as a VPC Gateway
Tested on 26 November 2020

To configure Droplets as internet gateways Follow everything in [Digital Ocean Blog.](https://www.digitalocean.com/docs/networking/vpc/resources/droplet-as-gateway/)

The above configuration will not work if you want to Turn Off  the public network interface `eth0`, because the blog show how to send the traffic over `eth0` and not private network interface `eth1`. To send internet traffic over 'eth1' use the following command in your backend droplet instead of the one in the Digital Ocean Blog. 
```
ip route add 169.254.169.254 via <your-gateway-private-IP> dev eth1
```
