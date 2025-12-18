# AlphaLite
Full featured single node RotorHazard timer

Usage Information

Power

There are two inputs to the device; a USB C connector and an MR30 connector. Both inputs are directly connected together. DO NOT connect power input at both connectors at the same time!

Unit will power on when it receives 5v at either input. You may shut the unit off by using the shutdown button in the RotorHazard admin page, or pressing and holding the button on the bottom of the unit labeled "shut" for 4 seconds. Once the green light on the top of the unit(pi) turns off ~10sec, you may safely unplug your unit. 

At power on(plug in), you will first be greeted by a green? led on the bottom of the unit to indicate a valid power supply. the white light on the bottom of the unit represents the stm32 processor activity. It should be slowly blinking white. Once/if pi has succesfully booted and the RotorHazard server has launched, you will be greeted by rgb.. once connected to the RotorHazards web server the stm32 led should be rapidly blinking.

Connect

   Wireless - WiFi
   
The pi is running a script named accesspopup to handle automatic wifi hotspot. More info available at https://www.raspberryconnect.com/projects/65-raspberrypi-hotspot-accesspoints/203-automated-switching-accesspoint-wifi-network
please read it!
   
When the pi boots up, it will first try to connect to a known local wifi network. If no known network is available, the pi will start its own wifi hotspot. You can access this hotspot with these credentials
   Name: alphaLite timer
   Password: password

   Wired

You may connect to a wired network in two ways. 
First, you may power the unit via its mr30 connector and then connect a simple ethernet to usb c adapter.
You may also choose to use an ethernet + poe to usb c + pd converter to supply both power and data to your unit over one cable.

Control

When connected to the timer via its local hotspot, you may connect to it @    IP address: 192.168.50.5
This ip address may be used to ssh, or sftp into the timer should you need.
   Username: administrator
   Password: password

The RotorHazard server will be available @
IP address: 192.168.50.5:5000
via your web browser.
   Username: admin
   Password: rotorhazard

When connected to a known wifi network you must currently determine your own IP address. No static IP is currently implemented.

RGB LED!

The unit provides a 5v logic RGB led control output, compatible with ws2812 etc on the MR30 connector. 
Our preference is that you DO NOT power your leds through the unit. However, the unit is specified to condfidently handle the maximum current availabe in the USB spec of 3A @ 5v passed from USB through to the MR30 output, if your power source is capable.
The unit itself needs ~1A, more at startup.
This should leave enough to run a 24" flag pole of about 34 leds at max brightness or a RaceGOW gate of 110 leds at medium brightness.
You are responsible for safe operation of your unit. An led power draw calculator can be found at https://wled-calculator.github.io

Hardware Info

The stm32f103 is connected to the Raspberry Pi Zero 2 W via its primary UART. Under RotorHazards advanced settings you will need to set the node address as "/dev/serial0"; "serial0" alone is not sufficient and may cause a lockout requiring you to manualy delete the config.json file to restore operation. 
