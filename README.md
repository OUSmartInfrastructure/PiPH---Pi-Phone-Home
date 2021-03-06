# PiPH - Pi-Phone-Home
Pi Phone Home - System to have RasPi (or any system) relay system details to a central location on a schedule.

Needed a way to know the DHCP IPs of RasPi without access to DHCP Server logs. As they moved around to different subnets. 

This system uses FTPS (Filezilla Server) to have the unit push details up to the server. It creates a file based on the Pi's MAC address.

The index.php is located in the same directory as uploaded files. HTTP/PHP will need to installed for web display of data (IIS was our platform). 

To install with git, please cd into the /usr/local/bin folder.

cd into /usr/local/bin/PiPH

Please run within the directory folder.
sudo chmod u+x install.sh
sudo ./install.sh 

We will use lftp as our ftps client that shall be running with a self-signed certificate.
The install script will run:

sudo apt install lftp

sudo nano /etc/lftp.conf --- add lines: set net:reconnect-interval-base 0 & set ssl:verify-certificate no into the bottom

We set verify-certificate to no, because we do not need to verify our self-signed certificate, as this will throw an error within the LFTP software.

![alt text](https://raw.githubusercontent.com/OUSmartInfrastructure/PiPH/master/Images/LFTP_Configuration.PNG)

sudo crontab -e --- add line:  * * * * * [path to files]

![alt text](https://raw.githubusercontent.com/OUSmartInfrastructure/PiPH/master/Images/Crontab-command.PNG)

![alt text](https://raw.githubusercontent.com/OUSmartInfrastructure/PiPH/master/Images/Crontab.PNG)

piph.conf file has following format:

Host:yourftpsserver.com

Username:pi

Password:raspberry

Interface:eth0
![alt text](https://raw.githubusercontent.com/OUSmartInfrastructure/PiPH/master/Images/Configuration_file.PNG)
