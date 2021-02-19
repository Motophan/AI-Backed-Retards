Why:

Traefik ssl labs a+ (breaks win 7 ie8 beware) will be compatible w/ 2.5 http3 udp quic w/ expiramental flag (not available in 2.4)

This is my responce to all the competing seedbox provisioning scripts. I dont like any of them. This teaches you how to intergrate your own provisioning script by teaching you compose. I can comment the crap out of the code if it doesnt make sense, if anyone is reading this. 
The least bad of all of them is probabally swizzin, use that.

Cloudbox -> permbanned me from their discord when I pushed hard for a traefik fork and explained why they broke ipv6. I was not polite, I regret this. 
That being said, I am no longer welcome with them. This is what I stole/made to make some working implementation they could throw into ansible.
Rumor has it they are not going to traefik. :/ 

Swizzin -> nginx backends are 127.0.0.1 so IPv6 """"""""works""""""" with a asterisk the size of the planet jupider. Its not ideal.

Quickbox -> just no. 

Swag + linuxserver -> very very good implamentation but same problem as swizzin. Can we please move to sockets? Also, permbanned from their discord because I tried to explain how they broke my nextcloud. I was not polite. I regret this. :/

Unraid -> no ipv6, very very difficult to fix, devs dont care, nonfree


How to use:

1- edit .env file to reflect your setup
run `id` and make the PUID = your ID, and the GUID = dockers ID
this is so your containers run in usermode

2- add containers by copying and pasting the stuff. All you change for traefik is 
```
labels:
      - "traefik.enable=true"
      - "traefik.http.routers.appname.rule=Host(`appname.$DOMAINNAME`)"
      - "traefik.http.routers.appname.entrypoints=websecure"
      - "traefik.http.routers.appname.tls=true"
      - "traefik.http.routers.appname.tls.certresolver=resolver"
      - "traefik.http.routers.appname.middlewares=security-headers"
      - "traefik.http.routers.appname.tls.options=default"
#      - "traefik.http.services.appname.loadbalancer.server.port=80"
    networks:
      - yeetmaster
 ```
      
You dont actually need the last line. Traefik is properly setup so its pretty good about figuring itself out. If it fails, just explicitly set the port. Whatever.

