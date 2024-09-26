## Installation and Configuration PowerMTA on Linux

#### Install the requirments for Install PowerMTA
For Ubuntu OS
####
    apt install unzip net-tools telnet git gdb -y
For Centos OS 
#### 
    yum install unzip net-tools telnet git gdb -y
####
If you already have a mail server remove it.
####
For Ubuntu OS
####
    apt remove postfix -y
####
For Centos OS
####    
    yum remove postfix -y
####   
If you want to keep current mail server, you can run PowerMTA on a port other than 25 <br>
Make a directory in /root
####
    mkdir pmta /root
    cd /root/pmta
####
Download PowerMTA
####
    wget https://www.rekblog.com/tools/pmta.zip
####
Download powermta config file
#wget https://vkttech.com/wp-content/uploads/2020/07/powermta-config.zip
####
Unzip to downloaded file
####
    unzip pmta.zip pmta
#unzip powermta-config.zip
####
Check files
####
    ll

#Now install PowerMTA
#1st way to execute the install.sh file where are autoscipted.
./install.sh

#2nd way to execute the rpm file, after will need to manually configure.
rpm -ivh PowerMTA-4.5r8.rpm

#If we are on Debian Based OS then use this command
apt-get update -y
apt-get install alien -y
alien -i PowerMTA-4.5r8.rpm --scripts

#When install on ubuntu/debian then following some task from install.sh:
mv license /etc/pmta/
rm -rf /usr/sbin/pmtad
mv pmtad /usr/sbin/
chmod 750 /usr/sbin/pmtad
chown pmta:pmta /etc/pmta/config
chmod 640 /etc/pmta/config
mkdir -p /var/spool/pmtaPickup/
mkdir -p /etc/pmta/domainKeys/

#Check pmta services
service pmta start
service pmtahttp start
service pmta status
service pmtahttp status

#If you get any error, run powermta in debug mode
pmtad --debug

#Modify pmta config to allow access config file via browser.
nano /etc/pmta/config

#Find http-access and add：
#192.168.56.104 is your own IP address.
http-access 192.168.56.104 admin    

#After editing config file, you need to restart PowerMTA
service pmta restart
service pmtahttp restart

#Or reload pmta services
service pmta reload
