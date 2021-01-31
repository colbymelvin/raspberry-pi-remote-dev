1. [Download VSCode](https://code.visualstudio.com/docs/?dv=osx) if you don't already have it.
1. Install and enable the [VSCode Remote Development plugin](https://github.com/Microsoft/vscode-remote-release).
1. Following the [documentation on connecting to a remote host](https://code.visualstudio.com/docs/remote/ssh#_connect-to-a-remote-host), connect to your Raspberry Pi via SSH with `ssh pi@yourhostname.local`.
    - This will install VSCode server components on your Raspberry Pi and connect to them.
1. Once setup, open your Raspberry Pi's remote file system in the explorer by clicking "Open Folder" and selecting a directory.
    - This will default to `/home/pi`. If you do not wish to setup your development environment(s) in the root directory on your Raspberry Pi, SSH into the Raspberry Pi via a terminal and run `$ mkdir Development`. Then, select `/home/pi/Development` as your workspace directory in VSCode.
1. Install and configure git on your Raspberry Pi.
    - `sudo apt-get update`
    - `sudo apt install git`
    - `git config --global user.name "Your Github Name"`
    - `git config --global user.email "Your Github Email"`
1. If you connect to GitHub via SSH, follow their [guide to setup ssh](https://docs.github.com/en/free-pro-team@latest/github/authenticating-to-github/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent) to generate a new SSH key and associate it with your GitHub account.