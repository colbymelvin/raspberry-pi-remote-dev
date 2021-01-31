## Step 4 - Basic Security and Cleanup

### Cleaning up WiFi network setup artifacts

In a previous step, we saved a plaintext representation of our Wifi network's password into `wpa_supplicant.conf`. In this step, we'll encrypt that information.

1. While SSH'd into the Raspberry Pi, change to the root user with `$ sudo su` and change to the root directory with `$ cd ../..`.
1. Use the `wpa_passphrase` utility to generate an encrypted PSK with and save it to the necessary configuration file with `$ wpa_passphrase "<YOUR_WIFI_NETWORK_SSID>"`
    - You will be prompted for the network's passphrase.
1. Issue the command `$ nano /etc/wpa_supplicant/wpa_supplicant.conf` and replace the `psk` in the `network` block with the new encrypted `psk` that was output from the previous step.
1. Restart your Raspberry Pi by typing `$ shutdown -r now`.
1. Wait for your Raspberry Pi to boot again - you can monitor this with `$ ping raspberrypi.local` (once requests stop timing out and you see data being sent successfully, your Raspberry Pi is back up and running).
1. SSH back into the Raspberry Pi with `$ ssh pi@raspberrypi.local` or `$ ssh pi@<RPI_IP_ADDRESS>`, and check wireless connectivity with `$ iwconfig | grep "wlan0"`
    - You _should_ see output like `wlan0     IEEE 802.11  ESSID:"<your_wifi_ssid>"` if we were successful.
    - If we weren't successful and you don't have wireless connectivity, check for the existence of a `wlan0` device with `$ ifconfig -a`.
        - If you see a `wlan0` entry here, it means that you do have a wireless device, but it's inactive. 
            - Try to bring up the device with `$ sudo ifconfig wlan0 up`.
            - If you see output like `SIOCSIFFLAGS: Operation not possible due to RF-kill`, that means the wireless device is either _hard_ or _soft_ blocked. Attempt to unblock it with `$ sudo rfkill unblock wifi`, then try to bring the device up again with `$ sudo ifconfig wlan0 up`.

### Changing Raspberry Pi defaults

1. 

1. (Optional) If you wish, now would be a good time to give your Raspberry Pi a different hostname. Since the default hostname for every Raspberry Pi is `raspberrypi`, setting up a new hostname now will help you down the road if you ever want to setup additional Raspberry Pis. You can do this by issuing the `$ sudo raspi-config` command, and following the GUI instructions to setup a new hostname.
    - After rebooting, you will now SSH into your Raspberry Pi with `ssh pi@<your_new_hostname>.local`.