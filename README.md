# Roomba-polyglot
This is the Roomba Node Server for the ISY Polyglot V2 interface.  
(c) fahrer16 aka Brian Feeney.  
MIT license. 

This project functions with Roomba WiFi enabled vacuums running version 2 firmware.  Currently, Roomba 980, Roomba 960, Roomba 890, and Roomba 690.

Roomba vacuums have a local interface reverse-engineered in the following projects.  Without the efforts of those developers, this project would not have been possible.
 * https://github.com/koalazak/dorita980
 * https://github.com/NickWaterton/Roomba980-Python

You'll need to use a static IP address for each Roomba or else the connection won't work each time the IP address changes.  Either set a static IP through Roomba app or through router.

The Roomba980-Python Github linked above explains the limitations of connections to Roomba vacuums.  This node server is configured to keep a constant local connection to each vacuum.  Only one location connection is possible but it is still possible to use the app with a cloud connection to the vacuum.  I recommend preventing the Roomba's from reaching the internet though, so that they don't update their firmware automatically to a version not compatible with this node server.
 
# Installation Instructions:
1. Add Node Server into Polyglot instance.
  * Follow instructions here:  https://github.com/Einstein42/udi-polyglotv2/wiki/Creating-a-NodeServer 
  
2. For each vacuum, a configuration item needs to be added to the Polyglot Node Server configuration:
  2.1.  Follow instructions here for obtaining roomba blid and password needed for configuration: https://github.com/NickWaterton/Roomba980-Python
  2.2.  Use a key starting with "vacuum" (e.g. vacuum1, vacuum2, etc...)
  2.3.  Key value format: {"ip":"192.168.3.36", "blid":"6945841021309640","password":":1:1512838259:R0dzOYDrIVQHJFcR","name":"Upstairs Roomba"}  Note the use of double quotes
   
## Version History:
1.0.0: Initial Release
1.1.0: Only update WiFi strength in ISY if the reported value has changed by more than 15% since the last update
1.1.1: Corrected display name of parameter 'GV7' from 'Bin Present' to 'Bin Full'

## Known Issues:
1. Commands that allow for a parameter value to be passed don't seem to be present in admin console unless the profile is uploaded twice.  May be an issue with ISY994i (This was developed using version 5.0.10E).
2. Base Roomba980-Python project allows for a dynamic map to be drawn.  This node server does not yet implement that functionality.
3. Roomba values are currently updated every 5 seconds (unless shortPoll duration is changed).  There could be a bit of a lag when issuing command or changing parameter values before they're updated in the ISY.
