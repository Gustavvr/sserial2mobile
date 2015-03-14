# Introduction #
This library was written with all the AT+ command stored in header file.  This should make it relatively easy to get the library to work with other phones.

# Phone #
**c168i.h**

The command for sending the SMS and emails is roughly the same on most phones.  In many cases these command should not have to be altered should not have to be altered.

_Any changes to any of the library files require the deletion of **SSerial2Mobile.o** and a restart of the Arduino IDE to force a recompile of the library_

# Carrier #
**att.h**

The carrier header file lists the number that the specific carrier uses to forward emails to the carrier's email gateway.  This number **will** need to be change to be correct for the specific carrier.  Unless you use the same carrier I chose.

_Any changes to any of the library files require the deletion of **SSerial2Mobile.o** and a restart of the Arduino IDE to force a recompile of the library_


# The Phone and Carrier I chose and why #

In the NYC,US ,area in which I live, popular stores like Radio Shack and Best Buy sell a Motorola C168i.  This phone cost ~$15 without a contract or even activating service.  Included with the phone is a SIM card. Money can be added to this prepay account through the carrier's web page.

I put $20 on the account for my tests. Each SMS or email cost $0.15.  An unlimited plan can be purched for ~$20/mo


_Prices are approximate as of Spring/summer 2008 in NYC,US_