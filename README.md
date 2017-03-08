# AirBlocker
A simple bash script to turn off MacOSX Airport when the computer is connected to a network adapter. 

This is a personal adaptation of the original gist from [albertbori](https://gist.github.com/albertbori/1798d88a93175b9da00b)
My own modifications make it work with my Chinese USB Ethernet adapter.


This is script will automatically turn your wifi off if you connect your computer to an ethernet connection and turn wifi back on when you unplug your ethernet cable/adapter. If you decide to turn wifi on for whatever reason, it will remember that choice. 


## Requirements

- Mac OSX 10+
- Administrator privileges

## Installation Instructions

1)If you have a macbook with integrated Ethernet card you can jump this:

  Before installing the script please edit the toggleAirport.sh script at the third line.
  Now the variable *ethAdaptID* is set to grep any possible Ethernet Adapter wich name ends with "Ethernet".
  Run this command: (Fig.)
  ```
  networksetup -listnetworkserviceorder
  ```
  And take note of the name of your ethernet adaptor and replace it in the script.
  In my case: `ethAdaptID=".*Ethernet"` becomes ethAdaptID="USB 10/100 LAN"

![fig1](https://www.dropbox.com/s/4uy5u9bretyghbz/Screenshot%202017-03-08%2011.42.51.png?raw=1)

2)Copy and change permission of the files:
- Copy `toggleAirport.sh` to `/Library/Scripts/` -> `sudo cp toggleAirport.sh /Library/Scripts/'
- Run `sudo chmod 755 /Library/Scripts/toggleAirport.sh`
- Copy `com.mine.toggleairport.plist` to `/Library/LaunchAgents/`-> `sudo cp com.mine.toggleairport.plist /Library/LaunchAgents/`
- Run `sudo chmod 600 /Library/LaunchAgents/com.mine.toggleairport.plist`
3) Start the watcher.
- Run `sudo launchctl load /Library/LaunchAgents/com.mine.toggleairport.plist` to start the watcher

## Uninstall Instructions

- Run `sudo launchctl unload /Library/LaunchAgents/com.mine.toggleairport.plist` to stop the watcher
- Delete `/Library/Scripts/toggleAirport.sh`
- Delete `/Library/LaunchAgents/com.mine.toggleairport.plist`
- Delete `/private/var/tmp/prev_eth_on`
- Delete `/private/var/tmp/prev_air_on`

## Misc

To debug, just run: `sudo /Library/Scripts/toggleAirport.sh` and add echo's wherever you'd like
