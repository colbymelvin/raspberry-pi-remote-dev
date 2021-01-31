## Step 2 - Setting up WiFi on your Raspberry Pi

Settings up WiFi on a headless Raspberry Pi is fairly straightforward. It involves the addition of a `wpa_supplicant.conf` file to the `boot` folder of Raspbian.

1. Create a `wpa_supplicant.conf` file in the root of the `boot` folder on the SD card.
1. Enter the following lines:
```
country=<Insert 2 letter ISO 3166-1 country code here>
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1
network={
  ssid="YOUR_WIFI_NETWORK_SSID"
  psk="YOUR_WIFI_NETWORK_PASSWORD"
}
```
1. Note that the `psk` we used is a plain-text representation on your WiFi network's password. We'll fix this and encrypt it in a later step, after being able to SSH into the Raspberry Pi.
1. Note that the Raspberry Pi can also connect to hidden networks, with the addition of `scan_ssid=1` to the `network` block above.