## Step 4 - Setting up WiFi on your Raspberry Pi

1. While SSH'd into the Raspberry Pi, change to the root user with `$ sudo su`.
1. Use the `wpa_passphrase` utility to generate an encrypted PSK with and save it to the necessary configuration file with `$ wpa_passphrase "<your_wifi_ssid>" >> /etc/wpa_supplicant/wpa_supplicant.conf`.
    - You will be prompted for the network's passphrase.
1. Type ctrl + d to change back to the `pi` user.
1. Issue the command `$ sudo nano /etc/wpa_supplicant/wpa_supplicant.conf` and insert the following lines at the top:
```
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
country=<Insert 2 letter ISO 3166-1 country code here>
```

4. Also take this opportunity to delete any lines from Step #2 that are commented out, namely the plaintext representation of your network's passphrase.

1. Restart your Raspberry Pi by typing `$ sudo shutdown -r now`.

1. Wait for your Raspberry Pi to boot again - you can monitor this with `$ ping raspberrypi.local` (once requests stop timing out and you see data being sent successfully, your Raspberry Pi is back up and running).

1. SSH back into the Raspberry Pi with `$ ssh pi@raspberrypi.local` or `$ ssh pi@<RPI_IP_ADDRESS>`, and check wireless connectivity with `$ iwconfig | grep "wlan0"`
    - You _should_ see output like `wlan0     IEEE 802.11  ESSID:"<your_wifi_ssid>"` if we were successful.
    - If we weren't successful and you don't have wireless connectivity, check for the existence of a `wlan0` device with `$ ifconfig -a`.
        - If you see a `wlan0` entry here, it means that you do have a wireless device, but it's inactive. 
            - Try to bring up the device with `$ sudo ifconfig wlan0 up`.
            - If you see output like `SIOCSIFFLAGS: Operation not possible due to RF-kill`, that means the wireless device is either _hard_ or _soft_ blocked. Attempt to unblock it with `$ sudo rfkill unblock wifi`, then try to bring the device up again with `$ sudo ifconfig wlan0 up`.

1. Once you have verified wireless connectivity on your Raspberry Pi, kill your SSH session and disconnect the ethernet cable from the Raspberry Pi.
    - (Important) Go back into System Preferences -> Sharing and disable Internet Sharing via Ethernet.

1. For sanity, go ahead and verify that you can SSH into the Raspberry Pi wirelessly. 

1. (Optional) If you wish, now would be a good time to give your Raspberry Pi a different hostname. Since the default hostname for every Raspberry Pi is `raspberrypi`, setting up a new hostname now will help you down the road if you ever want to setup additional Raspberry Pis. You can do this by issuing the `$ sudo raspi-config` command, and following the GUI instructions to setup a new hostname.
    - After rebooting, you will now SSH into your Raspberry Pi with `ssh pi@<your_new_hostname>.local`.