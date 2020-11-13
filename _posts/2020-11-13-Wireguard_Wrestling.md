---
layout: post
title: Wireguard and MacOS
author: Mac
---

I'd been dipping in and out of trying to get a VPN setup so that my phone is always connected into my home to talk to home IoT devices, 
(like a Philips Hue), my NAS box, in home cameras, etc.
With regards to IoT devices in the home I fundamentaly object to being forced 
to use a cloud service to essentialy solve the end to end networking problem that the extensive use of NAT in IPv4 has given us.
This is both based on the
architectural principle that it's stoopid, and on privacy and cybersecurity grounds - these systems somtimes, but not always, 
use TLS for the communications with the server, but rarely do end to end encryption, so the server is a weak spot.

<img align="right" src="/images/Slide1.png" alt="network" width="500"  />
<p>
We have choosen WireGuard in the
<a href="https://www.horizon.ac.uk/project/tangible-security-project/">TANSEC project</a> as we 
are keen to play with physical interactions as a way to establish a permanent bonding between your
phone and your home network, and with both the out-of-band nature of the Wireguard key exchange and the
"permanent" keys with no requirement for per session login involving a user, it was the obvious choice.
(Neverminding the Wireguard fans pointing out it many other benefits such as small code base, speed, modern crypto, etc.)
</p>

<p>
 This <a href="https://barrowclift.me/post/wireguard-server-on-macos">excellent article</a>
by Marc Barrowclift finally clarified WireGuard configuration  for me. Indeed I realised that for my setup,
it was even simpler than his configuration. However, I do end up with a non-optimal forwarding loop as most of 
the IoT devices we are talking about can only ever send things not on the local network to the default router assigned 
to them by the DHCP, and even if you could add static routes or indeed fire up routing demons in some places (like the NAS),
who could be bothered for such marginal bandwidth efficiency gains. Anyway as I have 
a Unity Ubiquiti router (and switches and WiFi), 
which does actual, err, routing, so I can easily deal the routing problem there. It'll do
 until the TANSEC project gets it all built in an <a href="https://openwrt.org">OpenWRT</a> router.
</p>

<img align="left" src="/images/Slide2.png" alt="network" width="500"  />
<p>So the basic setup: phone on 4G (or coffee shop WiFi) running standard Wireguard client,
home router configured to port forward default Wireguard port to internal iMac
running WireGuard "server" (from cmd line, not client in App Store), internal iMac set to IP forward,
router configured to forward WireGuard IP subnet back to iMac, some suitable dynamic DNS provider 
to ensure you can find your house.
</p>
<p>
I had the view from my previous fiddling around that the iPhone WireGuard client could only
route to the subnet of its interface address; well whether I just missed this or iOS has 
changed I dunno, but the client configuration of:
</p>


    Allowed IPs 192.168.32.0/20,192.168.16.0/24

adds the needed routing to the iPhone to forward the packets for the Home LAN over the WireGuard tunnel.

So here are the simplified (from Marc's setup) configurations you need. His "postup.sh" and "postdowdn.sh"
are not needed as we are not doign NAT, and the "server" configuration is simple, here "home.conf":

    [Interface]
    Address = 192.168.16.1/24
    PrivateKey = czcmzncnzmcnz,nczczn,msn-zncxz,ncaadunnnjhase
    ListenPort = 51820
    
    PostUp = /usr/sbin/sysctl -w net.inet.ip.forwarding=1  
    
    [Peer]        
    PublicKey = dsdkasjfa;sf;sfkdfa;kljdfklajdflajsdfkljaskf  
    AllowedIPs = 192.168.16.2/32  

while iPhone app confuguration:

    INTERFACE
    Name Home
    Public key dsdkasjfa;sf;sfkdfa;kljdfklajdflajsdfkljaskf
    Addresses 192.168.16.2/32
    
    PEER
    Public key aaduaiudnrinsrehifaurjfboasflsajfa;lj;asdfl
    Endpoint yourhost.dynu.net:51820
    Allowed IPs 192.168.32.0/20,192.168.16.0/24
    
    ON-DEMAND ACTIVATION
    On demand Cellular only

To fire it up automatically on your Mac, you need to follow Marc's instructions. 
In all it's working well, with the minor indigestion of the forwarding loop; and it's not 
really a general solution given many domestic routers would not let you add a static route.

I've seen Unity Ubiquiti community posts about installing WireGuard from the commandline, but 
there are only so many things I have time to mess with and getting into commandline stuff on
the router is not one of them.

I note that some coffee shops IP address assignment in 192.168 range might clash,
but they are nearly all 192.168.0.0/24 or 192.168.1.0/24, so if I do
find myself on a such a network and in dire need of home access, I'll just drop back to 4G.

Onward and upwards, IPv6 next.




