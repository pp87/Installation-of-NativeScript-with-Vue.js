# Installation of NativeScript with Vue.js

## Tested on Ubuntu 19.10 Eoan, set up as Virtual Machine in VirtualBox 6.0.20.

Most of the instructions come from the official manual https://docs.nativescript.org/angular/start/quick-setup, but it is incomplete/wrong in some places. I have 
created an issue for NativeScripts documentation here: https://github.com/NativeScript/docs/issues/1890

### Make sure that you have system up to date, with all the packages upgraded
```
sudo apt update
sudo apt upgrade
```

1. Download and install the latest LTS version of Node.js from https://nodejs.org/.
Restart your terminal and verify the installation was successful by running ```node --version```.
You can install Node with those instructions: https://github.com/nodesource/distributions#installation-instructions.
If you don't have ```curl``` you must install it: ```sudo apt install curl```
2. Install the NativeScript CLI
```npm install -g nativescript```
(You might need to do use ```sudo``` before ```npm install -g nativescript```)
3. Verify that the installation was successful by running ```tns``` in your terminal. You should see a long list of commands for ```tns```.

### Now the 'fun' part begins.
Set up android development environment, by modifing steps from this guide: https://docs.nativescript.org/angular/start/ns-setup-linux
1. ```sudo apt-get install lib32z1 lib32ncurses6 libbz2-1.0:i386 libstdc++6:i386```
2. ```sudo apt-get install g++```
3. ```sudo apt-get install openjdk-8-jdk```
4. ```sudo update-alternatives --config java``` and chose **Java 8**

So far things are nearly the same as in the main guide. Difference starts when you need to set up environment variables and android sdk.
Solution how to get things work, found here: https://stackoverflow.com/questions/60440509/android-command-line-tools-sdkmanager-always-shows-warning-could-not-create-se/61150826#61150826
1. Go to **Command line tools only** on https://developer.android.com/studio#Other and download **commandlinetools-linux-6514223_latest.zip**. File version can be different than this one at the moment of your installation.
2. Install android-sdk ```sudo apt install android-sdk```
3. Go to the folder you have saved the **commandlinetools-linux-6514223_latest.zip** file and unzip it

```sudo mkdir /usr/lib/android-sdk/cmdline-tools``` this folder will keep all required files

```sudo unzip ./commandlinetools-linux-6514223_latest.zip -d /usr/lib/android-sdk/cmdline-tools```

