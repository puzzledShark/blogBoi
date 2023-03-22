---
title: "Home Server Setup"
date: 2023-03-22
---

## I can talk about this without worrying about getting attacked right? lol

My homelab is made up of a simple structure of:
2 Nas Servers
One Server to handle all the processing

## Nas Servers

I'm not gonna out myself for what servers I bought but they're effectively off the shelf NAS servers, I know I could setup my own servers with unraid or such but I only want these to serve me files over samba, and to do it sipping as little power as possible as well as taking up little space so it was easier to just leave it to an off the shelf parts.

I have 2 because 1 is setup as an archive server which was cheaper and doesn't get accessed often while the other server is a much more expensive model with faster networking for my Intel Nuc to access.

Another thing to note about these servers is I setup rules in my routers to disallow access from outside the network, I don't need to access my files out of the network thus disabling this helps with cyber security, hopefully lowering the threat vector.

## Intel NUC Server

To handle all the processing I need done I purchased an Intel NUC that was fast enough to transcode subtitles for plex.

## Whats on the processing Server?

First of all, I decided on ubuntu linux LTS for the servers, my main reasoning behind this was that, due to its immense popularity, getting support would be much easier than with some of the more exotic linux varients, I do have some experience with centOS/redhat linux due to a previous job but that was so long ago I wouldn't count on it.

I setup  all the network directories to access the NAS servers over samba/cifs, that was easy enough.

My main purpose for this NUC when I bought it was to handle all my plex encodes 24/7 so i wouldn't have to have my main desktop on. I decided to install this as a native linux application.

Aside from plex I also wanted to setup a headless torrent server that I could send jobs to. For this I decided to use my knowledge of docker to execute some images, the images I used was transmission-openvpn, this would somewhat hide my torrent traffic. With that setup I could run Transmission-remote-gui on my main pc to send jobs to be done even if my main pc was offline.

Finally I setup an application called FlexGet which I also deployed with docker, a general tool to interface with RSS/usenets to download media on a scheduled basis, now just to cover my ass, I do have subscriptions to most of the services I download media from, but with SO MANY SERVICES these days I really just wanted to have a little more control of where I could watch it and how I could watch it. With flexget setup, it automatically seeded libraries that plex itself could see and setup for me to access that media from anywhere.

