# XmtrControl
Raspberry Pi based time clock to change transmitter power by time of day

Once you have your Raspberry Pi 3 initialized (memory expanded, locale, keyboard, etc), this
step-by-step guide will ensure all dependencies are covered.

1.	sudo apt-get update
2.	sudo apt-get upgrade
3.	sudo apt-get install python3-smbus pytz python3-pifacecad python3-pifacecadrelayplus
4.	git clone https://github.com/abelectronicuk/ABElectronics_Python3_Libraries.git
5.	sudo nano ~/.bashrc

Move to the end of the file and add:

PATH="${PATH}:/home/pi/ABElectronics_Python_Libraries/ADCPi"
export PATH

PYTHONPATH="${PYTHONPATH}:/home/pi/ABElectronics_Python_Libraries/ADCPi"
export PYTHONPATH

6.	Reboot

At this point, the RasPi is ready to run the script. Load it into the home directory and type in the rterminal:

python3 XmtrCtrl.py &

The script should begin and the LCD will first show correct time of day, and then display power in kilowatts and percent of licensed value.

After you’ve installed the control script (e.g., XmtrCtrl.py) in the home directory and have it working, you can set the Pi to run the script at boot time:

sudo nano /lib/systemd/system/myscript.service

Add the following text:

[Unit]
Description=My Script Service
After=multi-user.target

[Service]
Type=idle
ExecStart=/usr/bin/python /home/pi/myscript.py

[Install]
WantedBy=multi-user.target

sudo chmod 644 /lib/systemd/system/myscript.service

sudo systemctl daemon-reload
sudo systemctl enable myscript.service

sudo reboot

To check the service, do this:

sudo systemctl status myscript.service

