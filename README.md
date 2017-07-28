# Open Conference and Camp Networks using Open IEEE 802.1x

Open Conference and Camp Networks can use IEEE 802.1x for privacy by configuring a RADIUS server to allow any username and password.

This has the following benefits:
* Users can choose their own username and password, no administration
* Each user will have EAP TLS running, sessions based keys - privacy

## Introduction

Wireless networks are by definition very open, and can be sniffed. This has
obvious problems when technical users meet, since a lot of people know how to
sniff wireless. The standard way of securing wireless networks is by enabling
cryptography.

The main crypto used in wireless networks are WPA2-Personal and WPA2-Enterprise.
WEP is old, dont use at all.

The problems with WPA2-Personal is that all users share a key, preshared key,
WPA-PSK - which allows any user to capture wireless traffic, and decrypt using
tools like airdecap. It doesn't scale at all.

The problem with using WPA2-Enterprise has been that it requires a user
directory, often LDAP or Microsoft Active Directory is used in enterprise
settings. This would make it hard for people to get online, since an elaborate
sign-up procedure would be needed, and also registering people can be bad.

A few years back some conferences found they could configure the user directory
to allow any user with any password, and this would allow the use of
WPA2-Enterprise giving each user a session key with the wireless network easily.

BTW Who was the first to have this brilliant idea?

TL;DR
You can use any username/password combination using EAP-TTLS with PAP to login


## Configuring IEEE 802.1x - example

This repository is made as an example of the configuration we use at BornHack www.BornHack.dk

We have done lab experiments using some very easily obtainable systems:
* Unifi Access Point UAP Pro, should work with any of their APs I think
* Raspberry Pi using Debian Jessie 8.0
* Unifi Controller installed on the rPi
* FreeRADIUS 2.2.5+dfsg-0.2 - not a specific version, just the one we got using apt-get update

Testing devices Android phone, Macbook Pro, iPhone, ... various devices


## Installation Guide

1) First setup the wireless network using normal procedures, switches, APs etc.

2) Install FreeRADIUS

3) Change /etc/freeradius/eap.conf
First occurance of md5 is to be changed from md5 to ttls

4) Change /etc/freeradius/users
Remove most of the file - removing comments make it more readable

Add to the DEFAULT config
Auth-Type := Accept

TIP: see the directory freeradius for examples of the files, shown both as complete files and diff files

5) Test using the command
freeradius -X

Hint: you may need to stop freeradius first if already running, use:
service freeradius stop



Sources:
https://wiki.emfcamp.org/wiki/Network/802.1X_client_settings - example client configuration
https://events.ccc.de/camp/2015/wiki/Static:Network CCCamp 2015
https://en.wikipedia.org/wiki/Wi-Fi_Protected_Access
https://en.wikipedia.org/wiki/IEEE_802.1X


Interesting apps - for configuring Android
https://play.google.com/store/apps/details?id=tf.nox.wifisetup
