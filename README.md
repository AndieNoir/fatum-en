Fatum-2 Telegram Bot Configuration Manual


System Requirements:
.Net Framework 4.6.2. or higher


Warning: By using this software you automatically agree to take all responsibility of its usage and any consequences of its work. 
You agree that Developers of this software are not responsible for any effects of visiting generated locations or any other actions in the context of using this software. 
You agree that all users of this software can access any functionality provided, including settings changes, all types of random points generation and maintenance functions, and all that functionality you provide to them by your own will, regardless of whether you understand how it works or not.
You are free to modify and copy this software at your own risk. 


System Deployment:

0. Install .Net Framework 4.6.2. if you haven't.
1. Copy all files to your PC.
2. Set all necessary parameters in the config.txt file.
3. Start Fatumbot.exe (Bot will functioning while it works)


Configuration of config.txt file:

All values are set in square brackets.

1. At first, set new value to "MaintenanceKey" parameter. This key gives an access for remote administration of software and leaving it with the default value is highly insecure. It's like a password for entering a maintenance session.

2. If your provider is blocking telegram, you can set connection via proxy-server. Set "WebProxy" parameter to your proxy-servers URL, (for example "WebProxy [http://103.231.218.30:41098]"), and "proxylogin", "proxypass" to proxy-server credentials. If you are not using some of these parameters, set them to "none".

3. Set "TelegramToken" parameters value to the token for your telegram bot. You will be provided with one, after telegram bot registration in @BotFather.

4. "APPI" parameter affects the amount of points, used in attractor generation (Points per km of radius). We recommend to leave it as is.

5. "ConnTimeout" is a timeout of synchronisation with telegram. You can try to change it, but better not.

6. "RandomnessSource" is a Quantum source you are using to obtain random numbers. Following values are possible:
QRNG - Random numbers will be obtained from https://qrng.anu.edu.au/ . The random numbers are generated in real-time by measuring the quantum fluctuations of the vacuum.
REG - Psyleron REG-1 device will be used. But in this case, REG-1 should be connected to PC via USB cable. Do not use this option, if you don't have one.
Pseudo - No Quantum sources will be used, just the pseudo-random generator of your PC.

7. "LogfilePath" parameter is the path to the log file. You can set a custom destination and filename, or just filename to create log file in the same folder as fatum-bot.



HOW TO USE

To know, that the bot is working, send /test command to telegram bot's chat. It will respond "Fatum-2 is online".

To see instructions send /help command. You can also change instructions in "help.txt" file.
To restrict user from using bot's functionality, add his user_id to file "banned.txt" and restart Fatumbot.exe. Id's should be added as a column.
File "chats.txt" contains a list of all known user id's, interacted with bot.

Select the center of the map:

The Points will be calculated inside a given radius around the center. It is recommended to set your current location as a center.
By default calculation area is set to 10000m circle around Moscow.  
To change the area, you can send your current location via telegram mobile-app in-built function "Send location", it will be set as a map center.
If you are using Telegram Desktop, find desired location on Google Maps and sen a link to it like this:  https://www.google.com/maps/@54.9831153,73.3224661,21z
(The link should have the same format as in example)

Select area radius:

If the map center is your current location, area radius will be the maximum proximity to the target point. To change it, send command /setradius.
You will receive an answer: "Send new radius in meters (for example 3000)", send new radius then.
To drop settings to default, send command /setdefault.

Commands for Points generation:

/getpseudo - will send you a random location, generated by simple pseudorandom numbers generator (not quantum).
/getquantum - will send you a random location, generated by Quantum Random Numbers Generator source, set in configuration (by default it's QRNG - https://qrng.anu.edu.au/)
/getattractor - will send you an attractor point. For its generation a few thousands of quantum-random points will be created and then the program will find an area with maximum density of these points and calculate it's center as an attractor.
/getrepeller -  The opposite of the attractor point; A place with the minimum density of the point will be found.
/getpair - will send you both attractor and repeller points at once.

for deeper understanding read "theory.txt".


How to use maintenance functions:

Maintenance functions can be used if you need to adjust some settings in config.txt or to access log file remotely.

To enter maintenance session send your maintenance key with "mnts" command like this: "mnts MYSECRETKEY".
After that you will accept message "Key Accepted. Maintenance session started for user ****", 
meaning the system granted you with right to use mnts command features.

To close session and revoke that right from your account send "mnts close session" command.

Here the list of mnts commands:

Config.txt parameters change:

mnts change appi - allows you to alter APPI value. Can be used like this: "mnts change appi [200]".
mnts change timeout - allows you to alter ConnTimeout value. Can be used like this: "mnts change timeout [30]".
mnts change RNG source - allows you to alter RandomnessSource value. Can be used like this: "mnts change RNG source [REG]".
mnts change log adress - allows you to alter LogfilePathe value. Can be used like this: "mnts change log adress [C:\customfolder\log1.txt]".

Users restriction
To ban user from bot usage send command "mnts ban user [user_id]". To undo the ban send: "mnts unban user [user_id]".

To terminate Fatumbot.exe send "mnts terminate server".

Log operations

To dowload log.txt file send "mnts fetch [log.txt]", if you placed log file in custom location and don't remember it's name, you can download a list of files in log-folder like that: "mnts whosthere [C:\customfolder]". You also can check adress of fatum bot folder with command "mnts whereami".
