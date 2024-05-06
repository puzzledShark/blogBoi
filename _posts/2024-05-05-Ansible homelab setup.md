---
title: "Ansible Homelab Setup"
date: 2024-05-05
---

## Preface
I have something like a homelab setup at home, its mostly centered around Plex and automating aquiring content that I've legally purchased, but am too lazy to rip myself. That sounds relatively simple, but the way I've set it up its quite complicated.

## The Setup
I have 2 QNAP Nas's that manage my data, one is for backing up long term data, and the other is for more "hot" things, so its basically a hot/cold setup.
Then I have an intel NUC to handle all the processing.
The intel NUC runs wireguard and plex on "baremetal" and runs 2 docker containers, transmission, and flexget respectively.
This setup of mine is pretty fragile, I do have some docker compose files but that won't help with samba mount points and other things that I've done.

Before actually nuking my setup, I just picked myself up a lenovo m920q, it has more cores, and well, if anything goes wrong at least my NUC is still vanilla.

## The Proposed solution for orchestration
I waffled a bit with how I should really set this up.

First up I need some sort of orchestration to get my bare metal servers ready for my applications, since I still run some of my test application on bare metal instead of VM's.

Reading up a bit, the current hotness is between Ansible, puppet, and chef? This one was actually relatively easy because I already have experience with ansible, thats what I choose for prepping my bare metal servers.

## Ansible Inventory
In regards to ansible, its pretty simple, you just install the controller applications on a computer, and make some ansible files.

In ansible you create an inventory of hosts, I setup the hosts file with my NUC and my thinkcentre, this went relatively smoothly once I understood what ansible wanted.
By default ansible tries to login as your host user, so like Kenny@Host -> Kenny@server, took me a while to figure this out, but once I changed some of my inventory files with the correct users, and setup ssh-key-logins everything was smooth

With the inventory setup its time for the playbooks

## Ansible Playbook
This is the meat of what I wanted to do, if I set this up properly I'd have the means of setting up a baremetal server with everything I need which would be:

1. Setting up Software I'd need on the device
2. Setting up the samba shares to my NAS's to the device
3. Creating docker-compose files

Now that last one was a point of contention for me, I had considered using kubernetes, but the more I thought about it, for my fairly simple setup, where I'm the only person using it, is there really any point? I don't need scalablity.

Most of this went fairly smoothly, but I made a HUGE rookie mistake in regards to creating the docker-compose files

## Ansible files fumbles
As I'm extremely rusty in ansible, I can't say I made the smartest decisions at first, so here's my method for creating docker-compose files:
1. Go into host device, make folders
2. Do a copy command of the docker-compose to that folder
3. Run a regex command on that file looking for "keyword tags" i had embedded, and did a regex on that
4. Repeat step 3 as many times as I had embeded these tags

Now.... this feels like the common joke, where someone tries to determine even or odd with 100+ lines of if else code, and frankly it is basically that.

This way of doing it worked fine when there were 3 keyword tags to replace, but when I ran into a file with more than 10, I finally bonked myself on the head, and did some digging into the documentation and found out about templates.
Yes, templates, staring me right in the face, frankly I felt like a fool, the way it simplified it was astronomical.
It changed the steps into basically:

1. Create folder
2. Run templating engine, and place file in folder

Yeah thats right, I didn't even need to waste time on copying the vanilla docker-compose file onto the server.
Truly a marvel of engineering lol.

## Docker-compose?
Now I realize that theres ways to get docker-compose to work with ansible and all that jazz, but I wanted to keep it as simple as possible, I had all the variables for docker-compose seeded by ansible already, so all I really needed to do on bare metal was
run the docker-compose up, so I left that as is, its simple, it works!

## Docker issues
Now, part of what I wanted to do was to make this setup as modular as possible if I wanted to spin it up again, and I really wanted to put my plex config files on my NAS's but this is extremely frowned upon, I initally tried doing this, but thankfully my qnap nas does not support smb file locking, thus bricking my plex container and warning me about the extreme risk of putting config files on a remote location.

Since I still wanted to backup these files in case of disater, a simple cron job of backing up the plex config files was all it took.

## Docker Race issues
Now this part, is also my fault. With the way I have my NAS connections, they connect on boot, but at the same time docker tries to spin up.
Thus this is how it works out:

1. Docker/Smb connections start at the same time basically
2. Docker tries to mount volumes onto containers that the SMB connections have no finalized yet
3. Thus docker points to empty volumes onto my containers
4. Noone is happy

## Docker Race issue solution
Now, you're supposed to just create a mount on the fly for containers, thats the correct method, but I didn't want to do that because of other issues, so what did I do? I just told docker to not start for like a minute, this server basically restarts once a month for maintence, being delayed by 1 minute is perfectly fine.


## Conclusion

Well actually there is no conclusion, I'm still working on this.
So far most of it is working fine, but theres more to do if I want this to be truly modular and secure.

## Github link
https://github.com/puzzledShark/ansible-homelab-scripts

Thats where I tossed everything, I'm still working on it, but thats where it is