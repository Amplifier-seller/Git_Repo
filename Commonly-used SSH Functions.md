# Commonly-used SSH Functions ##
## 1. Connect to the server
Firstly, to establish a secret connection to the server, login the server via **ssh**:
```
ssh chengw@192.168.54.24
```
Type in the correct key, and you can now control the sever just as you wish. 
> Make sure that you have connected to the WLAN NIBS80M before you login.

## 2. Transferring wares between the server and your machine
Use **scp** command to realize the transferring. \
To send files to the server:
```
scp fileName.fileType chengw@192.168.54.24:/your/directory/
```
To get files from the server:
```
scp chengw@192.168.54.24:/your/directory/fileName.file.Type /your/machine/directory/
```

## 3. Display server windows on your machine
Config your machine's ssh X-tool first. edit `/etc/ssh/ssh.config`, find the items as below:
```
ForwardAgent yes
ForwardX11 yes
ForwardX11Trusted yes
```
Confirm that all the 3 items are set as 'yes' and there is no "#" before those items. If there is, delete it.
> "#" refers to annotation in this file.

After completing the configuration, enter the terminal, run the following command to allow the X-view of the server to connect to your machine:
```
xhost +192.168.178.50
```
> The IP address here should be your machine's current address. Type ifconfig -a in the terminal to find it.

Then run:
```
ssh -X chengw@192.168.54.24
```
Attention must be paid to that the "X" is in the capital form.\
Last but not least, export the server's X-view to your machine's display:
```
export DISPLAY=192.168.178.50:0.0
```
All done! Now you can make a test, e.g. run a `xclock` commad on your server, and you will find a clock showing on your machine if everything goes well.