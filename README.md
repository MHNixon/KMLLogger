KMLLogger is a platform-independent Lua script for X-Plane 11 & 12 which runs in FlyWithLua.
It is based on my original script MNFLightLogger from 2024.  If you are currently using that, then this is a drop-in replacement.
At the end of each flight it will create:
    • A detailed record of your flight in CSV format, which can then be imported into Excel, LibreOffice etc.  This shows dates, times, aircraft, departure & arrival airports, distance, flight duration, block times, fuel usage, altitudes flown etc. 
    • A record of your flight track in KML format, which can be opened in Google Earth.  This will show your horizontal and vertical profile in 3D, along with any waypoints you pass (Airports, VOR, NDB, Fixes etc).  At each waypoint you will be able to see exact status of your flight: ground speed, height agl, altitude, QNH etc).   This function is optional: you will be prompted at the beginning of your flight whether you want to log KML or not.
Requirements
    • You will need to install FlyWithLua: a simple, free, and extremely useful plugin.
    • Some functions will require Java.  A Java JRE is easily installed on all platorms
Installation
	Simply unzip the KMLLogger script into your /Resources/plugins/FlyWithLua/Scripts inside your main X-Plane folder.
Setup
    • No setup is actually required.  When the script starts, it will create a KML folder in your main X-Plane folder: your KML flight records will be saved in here.
    • To install FlyWithLua, follow one of these links: 
                • https://www.x-plained.com/flywithlua-for-x-plane-12/
                • https://forums.x-plane.org/files/file/82888-flywithlua-ng-next-generation-plus-edition-for-x-plane-12-win-lin-mac/
                • https://forums.x-plane.org/forums/topic/71006-howto-first-steps-using-flywithlua/
    • There are 2 macros, and you can assign keystrokes to the 2 functions:
            ▪ Show a status window (current flight details). Closes automatically after 20secs
            ▪ Show a window in which you can manually add a waypoint

Technical Stuff
    • With current settings, I did not detect any framerate drop when the script is running
    • Below 600m agl (+- 2000ft), the script will log status every 10 secs
    • Above 600m agl, the script will log once per minute
    • With autopilot on, a flightplan loaded, and flight director set to follow the track, the script will log each successive waypoint as it is passed.  For ZiboMod variants, as long as the script will log each planned waypoint as long as the flight director is on.  Waypoints logged are:
            ▪ Airport
            ▪ VOR
            ▪ Localizer
            ▪ Fix
            ▪ DME
    • With autopilot off, the script will search for and log any nearby waypoints matching:
            ▪ Airport
            ▪ VOR
            ▪ Localizer
            ▪ Fix
    • Certain waypoints can cause confusion, particularly runways, eg: “RW19”.  Consequently, these are not logged.
    • The csv  logfile will be updated provided the length of the flight exceeds 10 mins. 
    • Statistical logging:
            ▪ Starts with any engine on
            ▪ Ends with all engines off
            ▪ I have ignored the state of the parkbrakes, as some simmers may start their flights with engines already running
            ▪ With autopilot on when aircraft altitude = altitude dialled into flight director or...
            ▪ With autopilot off provided altitude remains constant for 5 mins or more, then flight altitude will be logged
            ▪ At end of fight, all altitudes logged in descending order of time spent at each altitude
            ▪ If your altitude has  not remained constant, then it will be logged as: “^~v” 
                (shorthand for “climb”, “variable altitudes” and “descent”)
    • At startup,  the script will disable the “use system time” option.  
           This means that you can speed up X-Plane as much as you like, but all times will be correct relative to each other.
    • The script uses states to determine its behaviour: on ground before, aloft after takeoff, back on ground. 
           So if you reload the script mid-flight, it will not function as designed. 
           At the start of a flight, you can reload the script, but once you have taken off,  
           reloading FlyWithLua scripts will mean you will lose all the data gathered by the script thus far. 
    • QNH.  If this is set incorrectly, all that will happen is that your altitudes logged will be out, 
           and even if flying with autopilot with dialled-in altitude, this may not be logged.
    • Altitudes are all rounded to nearest 100ft.  Normally +-50ft is the accepted norm for altitude hold as I understand, 
           but purely because this is a sim, and X-Plane 12 can be quite pernickety compared to X-Plane 11, I went with 100ft.   
           This mostly for VFR pilots
Filenames
    • The script is named KMLLoggern.n.n.lua Where n.n.n represent the full version number.  
            Subsequent updates will be named accordingly. When I post an update, simply download it and replace the previous version with the new one.
    • KML files are named by departure, destination airport icaos, plus date. Eg:
                • FACT-FAFK_20251102_0749.kml
                • FACT-FIMP_20251105_0744.kml
                • FAOR-EDDF_20260102_1914.kml
    • CSV logfile is named  FlightLog_n.n.csv. Where n.n represent the main and sub version numbers of the script.  
           The reason for this is that there may be changes to the csv layout from one version to another

Testing
    • As a pensioner, my finances are somewhat constrained, so I am unable to afford any of the really big commercial aircraft that I see on the market!  
       I will rely on you the user to alert me to any anomalies that may arise when flying any of these.  
       My script does rely on “vanilla” datarefs, so should work with pretty much any aircraft.
    • The 2 main aircraft types are those that use sim/.... based datarefs, and those like Zibomod which use laminar/B738 based datarefs.  
          The script copes with both types
    • I use Linux (Linux Mint Cinnamon 22.2), but as FlyWithLua, and Lua are both platform-independent, my script should work on Windows or Mac.
    • X-Plane 11:  C172, MD80, Piaggio P180, Laminar B737, Zibomod 737-800X, Pilatus PC12
    • X-Plane12: C172. Laminar B737, Zibomod 737-800X,  Cirrus SR22, Airbus A333


Tracing problems
If things go wrong, your first port of call is the X-Plane log file: Log.txt
This is in your main X-Plane folder, and is created by the sim itself, and contains very extensive logging data.
My script also writes to this file, so have a look through Log.txt to see if any errors are logged.
All entries will start with the word: KMLLogger

Credits
A special thanks go out to "wahltho", and many other helpful people on the various X-Plane forums.
Thank you all for taking the time to answer my questions.

Author:
Mike Nixon
mikenixon427@gmail.com
