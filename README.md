# VoiceonRPi4
Step by Step Tutorial on how to implement Voice Recognition on Raspberry Pi 4

-----------------------------------------------------------------------------------

Install the Pi AUI Suite by StevenHickson
https://github.com/StevenHickson/PiAUISuite
but do not run the command ./InstallAUISuite.sh <br>
sudo apt-get install libboost-all-dev <br>
Check the version by typing the command <b> ls /usr/lib/arm-linux-gnueabihf | grep 'libboost_regex' </b> <br>
Mine was 1.67.0 <br>
Type <b> sudo ln -s /usr/lib/arm-linux-gnueabihf/libboost_regex.so.1.67.0 /usr/lib/arm-linux-gnueabihf/libboost_regex.so.1.49.0 </b> <br>
<b> 1.67.0 </b> is the latest version that I installed and <b>1.49.0</b> is the previous version. Note that the versions may differ. <br>

------------------------------------------------------------------------------------------
Open PiAUISuite/VoiceCommand/speech-recog.sh <br>
Change <b>"-f cd -t wav"</b> to <b>"-f S16_LE" on the second last line </b> <br>
Open PiAUISuite/VoiceCommand/voicecommand.cpp <br>
Change <b>"-f cd -t wav"</b> to <b>"-f S16_LE" on line 34 </b> <br>
Open <b>PiAUISuite/VoiceCommand/tts</b> and replace the content with this code : https://github.com/StevenHickson/PiAUISuite/issues/56#issuecomment-205715002 (Note that this won't work until you Install Pico2Wave, instructions of which are given below) <br>
Run <b>make voicecommand</b> <br>
Go to PiAUISuite/Install and run the command <b>./InstallAUISuite.sh</b> 

<h2> To Enable Text-To-Speech </h2>
<h3>Install Pico2Wave </h3>
sudo apt-get install fakeroot <br>
Go to the home folder <br>
sudo apt-get build-dep libttspico-utils <br>
If the above code does not work , go to <br>
sudo nano /etc/apt/sources.list and uncomment the last line <br>
sudo apt-get build-dep libttspico-utils <br>
mkdir pico_build <br>
cd pico_build/ <br>
apt-get source libttspico-utils <br>
ls //Check the sox version <br>
cd svox-1.0+git20130326/ <br>
dpkg-buildpackage -rfakeroot -us -uc <br>
cd ../ <br>
ls *.deb <br>
sudo dpkg -i *.deb <br>
Now go on and check if it is working by using the <b>voicecommand</b> function <br>
<h4>You have successfully implemented voice recognition on your Rpi4!</h4> <br>
