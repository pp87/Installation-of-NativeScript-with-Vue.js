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
Set up android development environment, by modifying steps from this guide: https://docs.nativescript.org/angular/start/ns-setup-linux
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

4. ```cd /usr/lib/android-sdk/cmdline-tools/tools/bin```
5. ```sudo ./sdkmanager "tools" "emulator" "platform-tools" "platforms;android-28" "build-tools;28.0.3" "extras;android;m2repository" "extras;google;m2repository"```
6. When everything is done correctly set variables in ```.bashrc``` like this:
```sudo nano ~/.bashrc```
copy and paste the below:
```
export JAVA_HOME="/usr/lib/jvm/java-8-openjdk-amd64"
export ANDROID_HOME="/usr/lib/android-sdk/"
export PATH="${PATH}:${ANDROID_HOME}tools/:${ANDROID_HOME}platform-tools/"
export ANDROID_SDK_ROOT=/usr/lib/android-sdk
export PATH="$PATH:$JAVA_HOME"
export ANDROID_AVD_HOME=/usr/lib/android-sdk/.android/avd
```
7. You can make yourself links to ```sdkmanager``` and ```avdmanager``` like so:
```
sudo ln -s /usr/lib/android-sdk/tools/bin/sdkmanager /usr/local/bin
sudo ln -s /usr/lib/android-sdk/tools/bin/avdmanager /usr/local/bin
```
8. Reboot the machine.
9. Run ```tns doctor```, it should show somethign like this with success ticks:
```
✔ Getting environment information 

No issues were detected.
✔ Your ANDROID_HOME environment variable is set and points to correct directory.
✔ Your adb from the Android SDK is correctly installed.
✔ The Android SDK is installed.
✔ A compatible Android SDK for compilation is found.
✔ Javac is installed and is configured properly.
✔ The Java Development Kit (JDK) is installed and is configured properly.
✔ Local builds for iOS can be executed only on a macOS system. To build for iOS on a different operating system, you can use the NativeScript cloud infrastructure.
✔ Getting NativeScript components versions information...
✔ Component nativescript has 6.7.4 version and is up to date.
```

## Now you need to create virtual machine to emulate androis device and connect it with your development machine
Solution found here: http://umaranis.com/2019/06/13/setup-android-development-environment-on-virtualbox-vm/

