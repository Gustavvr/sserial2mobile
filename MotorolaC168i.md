![http://farm4.static.flickr.com/3254/2507585112_60cc338bfb_m.jpg](http://farm4.static.flickr.com/3254/2507585112_60cc338bfb_m.jpg)
# Making the cable #
On the top of the C168i is a 3/32 mini stereo jack.  This is also can be used as "hands-free" connection , but not both at the same time.  These 3/32 jack are usually stocked at Radio Shack [3/32" Stereo Plug](http://www.radioshack.com/product/index.jsp?productId=2062449&cp=&sr=1&origkw=3%2F32&kw=3%2F32&parentPage=search)

The solder point on the 3/32 plug are very small so it is probably a good idea to check for shorts with a multimeter.

In the picture I have used Ethernet CAT5 wire.  This is really not the best choice as it is not flexible but I just happen to have a lot of it around.

I will expand on this later but for now:

|**Plug**|**Function**|**Parameter in code**|**Represented in code**|
|:-------|:-----------|:--------------------|:----------------------|
|[Sleeve](http://en.wikipedia.org/wiki/TRS_connector#Tip.2Fring.2Fsleeve_terminology)|Ground|NA|NA|
|[Ring](http://en.wikipedia.org/wiki/TRS_connector#Tip.2Fring.2Fsleeve_terminology)|Phone TX/Arduino RX|First Pram.|SSerial2Mobile(<Arduino pin>,X)|
|[Tip](http://en.wikipedia.org/wiki/TRS_connector#Tip.2Fring.2Fsleeve_terminology)|Phone RX/Arduino TX|Second Pram.|SSerial2Mobile(X,<Arduino Pin>)|