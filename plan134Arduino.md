#Documentation and samples for plan13.

# Introduction #

Plan13.h - Will cacluate the curent location of many types of spacecrafts in an orbit (satlite/space stations/etc.) relitive to a specfic location on earth if provided with:
  * The specfic location ( longitutide and latitue)
  * The time ( time and Date)
  * A recent descirtipn of the satilite path in space (called a TLE)

> The libary will return the Azimuth and elevation where the spacecraft can be found.  Azmouth is direction(think compass) and elevation (degrese about the horizon (If I am looking at the horizan that is 0 degrees and if I am looking stright up that is 90{eleivation will never be more then 90))).

> This means an Azimuth of 180 degreese and 45 degree elevation would mean the object that is being tracked is directly south and 45 degreese above the horizon.

This library also calculates the dopler shift in the reciving and transmitting of the frequencies used with the spacecraft.

_Please forgive the use of "bird" the word satellite is just too long to keep typing :)_

# Example of use #
```
#include <Plan13.h>  //load satellite tracking library
Plan13 p13;                  //create an instance of a satellite tracking object

void setup () {
  p13.setFrequency(435300000, 145920000);//AO-51  frequency

  p13.setLocation(-64.375, 45.8958, 20); // Sackville, NB the location that will be tracked form

Serial.begin(38400);  set up the outgoing serial port on the Arduino

}
void loop() { 
  p13.setTime(2009, 10, 1, 19, 5, 0); //Oct 1, 2009 19:05:00 UTC

  p13.setElements(2009, 232.55636497, 98.0531, 238.4104, 83652*1.0e-7, 290.6047, 68.6188, 14.406497342, -0.00000001, 27022, 180.0); // keps for AO-51 //readElements();
  
  p13.calculate(); //crunch the numbers
  
  p13.printdata();  // print the location of the satellite 

 exit(1);         //end the program.  Just because we are neat programers
}
```
## The output will be like this: ##
```
AZ:57.08 EL: 3.98 RX: 435301705 TX: 145919429 Sat Lat: 53.87 Sat Lon.: 330.17 RR: -1.18
```


So if you were in New Brunswick Canada on Oct 10, 2009 at 19:05 UTC and looked a little East of North East (57.8deg) just at the horizon (3.98 deg).  Theoretically you would be looking at the satellite.  You directional radio antenna will detect it.




---

# void setTime(int yearIn, int monthIn, int mDayIn, int hourIn, int minIn, int secIn) #
## Description ##
This set the [UTC](http://en.wikipedia.org/wiki/Coordinated_Universal_Time) time] for the tracking. This can be in the future.  The calculated output with be the position of the bird at this time.  If looking for the when the bird will be visible (to the radio)  you probably want to calculates time into the future until you get an elevation of at least 5 degrees above the horizon. (because it is not feasible to transmit through the earth.)

For real-time tracking the value will need to be continuously updated and the `calculate()` function will need to be recalled each time.
> ## Parameters ##

int yearIn: the year in 4 digits e.g. `2010`

int monthIn: The month in 1 or 2 digits

int mDayIn: The month in 1 or 2 digits

int hourIn: The month in 1 or 2 digits

int minIn:The month in 1 or 2 digits

int secIn:The month in 1 or 2 digits
## Return Value ##
none
### Example ###
```
p13.setTime(2009, 10, 1, 19, 5, 0); //Oct 1, 2009 19:05:00 UTC
```

---


# void setLocation(double lon, double lat, int height) #
## Description ##
This is the location on Earth from where the bird with be observed.  Generally this is gonna be were your standing.  For real-time tracking the value will need to be continuously updated and the `calculate()` function will need to be recalled each time.
## Parameters ##
double lon: decimal degrees negative for west hemisphere

double lat: decimal degrees positive for north hemisphere

int height: in meters
## Return Value ##
none
### Example ###
```
p13.setLocation(-64.375, 45.8958, 20); // Sackville, New Brunswick Canada
```

---

# void setElements(double YE\_in, double TE\_in, double IN\_in, double RA\_in, double EC\_in, double WP\_in, double MA\_in, double MM\_in, double M2\_in, double RV\_in, double ALON\_in ) #
## Description ##
This is how the [orbital elements](http://en.wikipedia.org/wiki/Orbital_elements) of the satellite is set. Satellites are small things ( think compact car sized) moving around in a circle bigger the the diameter of the earth.  This means no matter how accurate the calculation are the tinniest of bit of imprecision in the math with cause the calculation to become less accurate over time.  Also, every other object in the universe is creating a gravitational pull on it.  This along with a host of other factors further adds error to the calculations.

So this means that very recent orbital elements are required that have the current corrections (your TLE data should be no more then a week old).  These are freely distributed by [NORAD](http://en.wikipedia.org/wiki/NORAD) and can be found for different types of space objects on the internet.  These can be easily found but doing an internet search for TLE.
## Mapping the TLE to this function prams ##
The TLEs (or two line elements) are actually generally 3 line with the top most one being the common name of the object.  The 2 lines of data contain specific information in specific columns of the line.  Below the line and the columns for each parameter is specified. You don't need to know what these mean but there are a of good resources on the web as well as the [ARRL Satellite handbook](http://www.arrl.org/shop/The-ARRL-Satellite-Handbook/)

Example TLE for the Space station
```
ISS (ZARYA)
1 25544U 98067A   08264.51782528 -.00002182  00000-0 -11606-4 0  2927
2 25544  51.6416 247.4627 0006703 130.5360 325.0288 15.72125391563537
```

_Note: The person writing portions of this doc is different from the person who wrote the library.  I can not begin to understand the math but I have no problems using the library. I just plug in the numbers form the TLE and use the results._

## Parameters ##
double YE\_in:  The year the TLE was generated.  The TLE only has the list 2 digits then need to be a 4 digit year.  **Line1 cols 19-20**

||double TE\_in: The day and fraction of the day the TLE was generated\*Line1 cols 21-32

double IN\_in: Inclination [Degrees](Degrees.md) **Line 2 Cols 09-16**

double RA\_in: R.A.A.N.     **Line 2 Cols deg 18-25**

double EC\_in: Eccentricity **Line 2 Cols deg 27-33**

double WP\_in:

double MA\_in:

double MM\_in:

double M2\_in:

double RV\_in:

double ALON\_in: SET to 0   _This is an artifact the the math algorithm.  it is not currently used_





## Return Value ##
none
### Example ###
```
 p13.setElements(2009, 232.55636497, 98.0531, 238.4104, 83652*1.0e-7, 290.6047, 68.6188, 14.406497342, -0.00000001, 27022, 180.0); // keps for AO-51
```
# void setFrequency(unsigned long rx\_frequency, unsigned long tx\_frequency) #
## Description ##
## Parameters ##
## Return Value ##
### Example ###
```
```

---


# void calculate(void) #
## Description ##
This causes the calculation to be run.  this will take about 12ms on an Arduino Diecimila.  This does not produce any output.  the variables must  be called directly
## Parameters ##
none
## Return Value ##
none
### Example ###
```
p13.calculate();
```

---


# void printdata(void); #
## Description ##
This will generate a brief but human readable output to the Arduino's serial output.  This is probably most useful for testing
## Parameters ##
none
## Return Value ##
non
### Example ###
```
p13.printdata();
```
## The output will look something like this: ##
```
AZ:57.08 EL: 3.98 RX: 435301705 TX: 145919429 Sat Lat: 53.87 Sat Lon.: 330.17 RR: -1.18
```

---




---

# int getDoppler(unsigned long freq) #
## Description ##
## Parameters ##
## Return Value ##
### Example ###
```
```

---
