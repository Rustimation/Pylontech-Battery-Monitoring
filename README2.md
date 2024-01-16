# Pylontech Wakeup Function for "C" Models like US2000C 
an addtion to and based on  
# Pylontech Battery Monitoring via WiFi by Ireneusz Kzielinski [https://github.com/irekzielinski/Pylontech-Battery-Monitoring]

An Instructable in German can be found at [https://rustimation.eu]

Some time ago, Ireneusz Kzielinski published his project on Github with which the battery can be monitored via WiFi. It essentially consists of an ESP8266 microcontroller (Wemos D1 Mini), a Max3232 transceiver, two capacitors, a remodelled network cable and a USB power supply. That's it! All essential information can be found on Github. Cost point 25 - 35€.

This allows the battery status to be read out interactively via a simple web interface and also manipulated within limits - for integration into IoT solutions, there is an optional MQTT or a small API that can also spit out the status information as JSON on request. Both can be easily integrated into Node-Red, Home Assistant or other IoT platforms.

I am assuming that you already have build the original board and are using Ireneusz' software. If not, please consult Ireneusz' project at Github [https://github.com/irekzielinski/Pylontech-Battery-Monitoring].

# Shutting Down The Battery
can be done by the existing software by issuing the command [http://IPAddress_of_D1_mini/req?code=shut]
However, afterwards you won't be able to restart the battery by means of the console software. 

# Restarting The Battery 
The Pylontech "C" models however, have two pins inside the console RJ45 port with a special purpose. If you supply a 5-12V, 5-15mA Signal for > 0.5 seconds to pin 4 (+) and pin 5 (-) you can restart the battery. If you build the little piece of hardware and use the code provided here, you will then be able to wake up the battery by issuing the command [http://IPAddress_of_D1_mini/wakeup]

# Extra HW Required
You already have the D1 Mini for Ireneusz solution, you'll need additionally
* 1 Logic Level n-channel MOSFET e.g. IRLZ44N or alternatively and possibly better IRF3708 (currently poorly available) or another Logic Level n-channel MOSFET
* 1 pull-down resistor with 47k Ohm
* 1 resistor with 220 or 320 Ohm
* Plus 1 pair of stacking headers - included in the D1 pack if you haven't thrown that away yet 😉
* 1 solderable terminal to attach the wires 4/5 that go to the console port.
* Small piece of dot/strip grid circuit board - preferably with 3 rows of dots - e.g. Rademacher 790
Cost is <5€

# Making a Piggyback Daughterboard
The board will go between the existing board from Ireneusz solution (assuming jou already have built it)
It looks like this:

![Piggyback board with attached D1 Mini to be plugged onto the original board](IMG_8643.jpg)

Provided that you haven't soldered the D1 Mini directly to the board. In that case you'll need to solder cables directly to the D1: +5V, Gnd, D5
The schematics are as follows:

![Schematics](Schematics.png)

# Code
I've added some lines to Ireneusz Code without touching the original logic. They are commented by text like "added by ...." 
Unfortunately I lack the Git/Github expertise to show the original solution and my additions side by side.
