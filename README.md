
# arducam libcamera klippper tutorial
your only guide to getting libcamera MPEG-Streamer Working with your klipper setup!

## DISCLAIMER
THIS TUTORIAL WILL NOT WORK WITH RASPBERRY PI OS "BUSTER"
MAKE SURE YOU'RE RUNNING RASPBERRY PI OS "BULLSEYE"
THIS ALSO WILL NOT WORK WITH UBUNTU OR OTHER DISTRO

THIS WILL WORK WITH SETUP INSTALLED BY KIAUH
IF YOU'RE USING OTHER METHOD OF INSTALLING KLIPPER AND IT'S COMPONENTS
SOME OF THIS MIGHT NOT APPLY TO YOU

this tutorial will work with Arducam 16mp AF camera
I'm not sure about other model, your milage may vary

### PART I, INSTALL ARDUCAM DRIVER
if you're using other model you might want to follow a tuorial for that model if you're running the same model as I do you can follow if you already installed the nessary packages and driver skip to PART II

1. cd back to your home directory
```
cd ~
```
2. Download arducam tool for installing packages and add execute permission to it
```
wget -O install_pivariety_pkgs.sh https://github.com/ArduCAM/Arducam-Pivariety-V4L2-Driver/releases/download/install_script/install_pivariety_pkgs.sh
chmod +x install_pivariety_pkgs.sh
```
3. install IMX519 Driver
after this process it will ask you to reboot, reboot before continueing
```
./install_pivariety_pkgs.sh -p imx519_kernel_driver
```
4. install libcamera packages
```
./install_pivariety_pkgs.sh -p libcamera_dev
./install_pivariety_pkgs.sh -p libcamera_apps
```
5. check if your raspberry pi detects the camera
```
ls /dev/video*
```
you should see video0 and video1
if not reseat your camera cable if that still dosent work I recomend rebooting the pi
if that still dosen't help get in touch with Arducam guys so they can try to help you!

### PART II, configure 
1. get MJPG-Streamer working
I will not show this process but you can install it using `kiauh`
2. download MJPEG-Streamer libcamera module from this repo
```
wget https://github.com/ChokunPlayZ/arducam-libcamera-klippper/raw/main/input_libcamera.so
```
3. copy the module into your MJPEG-Streamer directory
```
mv ./input_libcamera.so ./mjpg-streamer/input_libcamera.so
```
4. download webcamd file from this url to your computer
```
https://github.com/ChokunPlayZ/arducam-libcamera-klippper/raw/main/webcamd
```
5. open the file and edit the following setting using any text editor
edit line 8 and 9 with the username you're loggin in with in many case it will be pi
you can also edit focus setting, since autofocus is not currenly not supported you have to set the value manually
6. backup the old webcamd file with this command
```
sudo mv /usr/local/bin/webcamd /usr/local/bin/webcamd.bak
```
7. copy the contents of the webcamd you downloaded to your computer, make sure that you have put in the correct info
8. create a new webcamd file using
```
sudo nano /usr/local/bin/webcamd
```
9. paste the new webcamd file content into the nano window
 use `RIGHT CLICK` for windows command prompt and putty
 use `CTRL + V` for tabby terminal 
 10. save webcamd file
 just `CTRL + X` then `Y` then `ENTER`
 11. Add execute permission to webcamd file
 ```
 sudo chmod +x /usr/local/bin/webcamd
 ```
 12. add following content to your `webcam.txt` config file
```
camera_libcamera_options="-f 30 -r 640x480"
```
13. change this option in your `webcam.txt` file
```
camera="libcamera"
```
 14. restart webcamd service
 this process can be done in many way
 you can just run
 ```
 sudo systemctl restart webcamd
 ```
 to restart the service or you can reboot the pi
 I would suggest rebooting it
  ### Now you're set!
  ### Happy Printing!
  if you encounter any problem feel free to open an issue I will try to answer it as fast as possible
