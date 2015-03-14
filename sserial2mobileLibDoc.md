# SSerial2Mobile(rxPin, txPin) #
## Description ##
A call to SSerial2Mobile(rxPin, txPin) creates a new SSerial2Mobile object, whose name you need to provide as in the example below.
## Parameters ##
rxPin: the pin on which to receive serial data

txPin: the pin on which to transmit serial data
### Example ###
```
#define rxPin 2
#define txPin 3

// set up a new serial port
SSerial2Mobile phone = SSerial2Mobile(rxPin, txPin);
```

---

# SSerial2Mobile: off(void) #
## Description ##
Turn the phone's transmitter off.  Saves Battery
## Parameters ##
NONE
## Example ##
```
phone.off();
```

---

# SSerial2Mobile: on(void) #
## Description ##
Turns the phone's transmitter on.  On some phone this is actually a reset.  This should be hidden from the user of the library in the header files that contain the AT commands for each function.  see reset below
## Parameters ##
None
## Example ##
```
phone.on();
```

---

# SSerial2Mobile: reset(void) #
## Description ##
Resets the phone.  This can take a looooong time.  how long does the phone take to boot? My phone takes about 10 seconds
## Parameters ##
NONE
## Example ##
```
phone.reset();
```

---

# SSerial2Mobile: sendTxt(const char number[.md](.md),const char msg[.md](.md)); #
## Description ##
Sends a txt (SMS) message to another phone
## Parameters ##
const char number[.md](.md): The phone number
const char msg[.md](.md)): message.  ( MAX 160 char. as per SMS spec.)
## Example ##
```
phone.sendTxt("+15555550125","Lib SMS Test1");
```

---

# SSerial2Mobile: sendEmail(const char emailAddr[.md](.md),const char msg[.md](.md)) #
## Description ##
Sends email message to the internet
## Parameters ##
const char number[.md](.md): The email address
const char msg[.md](.md)): message.  ( MAX 160 char. as per SMS spec.)
## Example ##
phone.sendEmail("sserial2mobile@example.com", "Lib email test1");

---

# SSerial2Mobile: println(const char[.md](.md)) #
## Description ##
Prints data to the transmit pin of the software serial port, followed by a carriage return and line feed. Works the same as the Serial.println() function.

This is if you know what AT+ command you want to send
## Parameters ##
.println(str) if str is a string or an array of chars, prints str an ASCII string.
## Example ##
phone.println("AT+");

---

# SSerial2Mobile: batt #
## Description ##
As percent charged
## Parameters ##
NONE
## Example ##
> Serial.print("Batt: ");
> Serial.print(phone.batt());
> Serial.println("%");

---

# SSerial2Mobile: rssi #
## Description ##
http://en.wikipedia.org/wiki/RSSI

This should be about >=5 or so to send a message
## Parameters ##
## Example ##
> Serial.print("RSSI: ");
> Serial.println(phone.rssi());

---


---


---


---


---


# NOT YET IMPLEMENTED #

# SSerial2Mobile: ready #
## Description ##
## Parameters ##
## Example ##

---

# SSerial2Mobile: wait4OK #
## Description ##
## Parameters ##
## Example ##

---

# SSerial2Mobile: ber #
http://en.wikipedia.org/wiki/Bit_error_rate
## Description ##
## Parameters ##
## Example ##

---
