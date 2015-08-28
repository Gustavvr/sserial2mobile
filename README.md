# SSoftware2Mobile #
## An Arduino library to allow SMS and emailing via mobile phone ##
![http://farm4.static.flickr.com/3254/2507585112_60cc338bfb_m.jpg](http://farm4.static.flickr.com/3254/2507585112_60cc338bfb_m.jpg)


[| Full Size image](http://flickr.com/photos/rabbitnyc/2507585112/)

This library implements the Software serial Arduino library to establish a serial connection to a Mobile phone.  The methods methods hides the AT+ commands from the user allowing messages to be sent by passing the method on a phone number or email and the message.

- Gustav von Roth

Now with signal strength (RSSI) and battery monitoring.


PLEASE EMAIL ME IF YOU HAVE A PROJECT USING THIS.  I WOULD LIKE TO ADD IT TO THE WIKI


"Sserial2Mobile AT vonroth c-=-=-o-=-=-=m"


---

e.g.
```
SSerial2Mobile phone = SSerial2Mobile(2,3);

phone.sendTxt("+15555550125","Lib SMS Test1");
phone.sendEmail("sserial2mobile@example.com", "Lib email test1");

  Serial.print("Batt: ");
  Serial.print(phone.batt());
  Serial.println("%");
  
  Serial.print("RSSI: ");
  Serial.println(phone.rssi());

```
