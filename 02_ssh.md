## Step 2 - Enabling SSH access on the Raspberry Pi:

I prefer to use Raspberry Pis in headless mode, i.e. without peripherals. In order to do this effectively you will need to be able to SSH into your Raspberry Pi from your machine. Out of the box, Raspberry Pis have SSH capabilities, but these capabilities are disabled by default and must be enabled manually.

1. Insert the MicroSD card with Raspbian Buster Lite into the card slot on your computer, or a connected SD card reader.
1. Create a file titled `ssh` (no extension) with `$ touch Desktop/ssh`.
1. Copy this file from your machine to the `boot` folder of the SD card.
1. Eject the MicroSD card.
1. Check your machine for existing SSH keys with `$ ls ~/.ssh`; the presence of either a `id_rsa.pub` or `id_dsa.pub` file means you can skip the next step.
1. Generate SSH keys on your machine with `$ ssh-keygen`.
    - Save your key in the recommended location, `~/.ssh/id_rsa`.
    - You will be prompted for a passphrase, enter one if you wish.
    - (Optional) If you setup a passphrase, you can store that passphrase in the MacOS keychain with `$ ssh-add -K ~/.ssh/id_rsa`, which will allow you to connect with the Raspberry Pi without entering the passphrase.

----

## Step 3 - SSH into your Raspberry Pi

1. Insert the MicroSD card into the card slot on the Raspberry Pi, plug in your charging cable , and boot up the Raspberry Pi.
1. On your machine, enable "Internet Sharing" to computers using "Ethernet" via System Preferences -> Sharing.
1. Connect your Raspberry Pi to your machine via ethernet.
1. Head over to System Preferences -> Network and wait for an ethernet connection to be established via DHCP.
1. Once a connection has been established, install your machine's SSH public key onto your Raspberry Pi with `$ ssh-copy-id pi@raspberrypi.local`.
    - You will be prompted for pi@raspberrypi.local's password - the default password is `raspberry`.
    - Note the usage of `ssh-copy-id`; this installs your SSH public key to the Raspberry Pi as an authorized key, enabling passwordless SSH access to your Raspberry Pi from your machine. If your machine does not support the `ssh-copy-id` command, you can copy the key manually with `$ cat ~/.ssh/id_rsa.pub | ssh pi@raspberrypi.local 'mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys'`
    - Also note the usage of `raspberrypi.local`. If we're using a machine with Multicast DNS capability, we can resolve the IP address of the Raspberry Pi via the machine's hostname, provided the Rasperry Pi and machine are on the same network (which should be the case if you're following these instructions). If your machine does not support mDNS, you can discover the IP address of the Raspberry Pi with a networking tool like [Nmap](https://nmap.org/). Once you have the IP address of the Raspberry Pi, you can SSH into it via `$ ssh-copy-id pi@<RPI_IP_ADDRESS>`.
1. SSH into your Raspberry Pi with `$ ssh pi@raspberrypi.local` or `$ ssh pi@<RPI_IP_ADDRESS>`.