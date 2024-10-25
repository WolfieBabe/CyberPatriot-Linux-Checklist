# CyberPatriot-Linux-Checklist
  **Note: Try to do these steps in order as to not prevent yourself from later on**

1. Read The Readme
   
     Note down which ports, users, and protocols are allowed

 
2. **Do Forensics Questions**

     You may destroy the requisite information if you work on the checklist!


3. Update Management

    1. Open a new terminal and run `sudo nano /etc/apt/apt.conf.d/10periodic`. When the edit screen loads, change "APT::Periodic::Update-Package-Lists" value to 1. Then, save and exit.
      
    2.  Run `sudo apt-get update` and `sudo apt-get upgrade`


4. AntiVrius and RootKit Detection

    1. Open a new terminal and run `sudo apt-get install chkrootkit rkhunter`. Then, in order, run `sudo chkrootkit`, `sudo rkhunter --update`, and `sudo rkhunter --check`
    
    2. After that, run `sudo apt-get install clamav`. Then, go to https://gitlab.com/dave_m/clamtk/-/wikis/Downloads and download the appropriate package for your os. Go back to your terminal and install the package with `sudo dpkg -i Downloads/PLACEHOLDER.deb` or `sudo rpm -i Downloads/PLACEHOLDER.deb` as applicable for your os (make sure to replace PLACEHOLDER with the package's filename).
    
    3. Run `sudo freshclam` and `sudo clamscan –i –r --remove=yes /` then minimize this window as it will take over an hour

  
5. User Account Management

    1. Run `sudo getent passwd` cross-reference the users listed with the readme. If there are any users that shouldn't be there, check their files for information and then delete them using `sudo userdel --remove-home USERNAME_HERE` (**do not delete system users!!!*). To create a user, use `useradd -u UID_HERE -d HOMEDIR_HERE -s DEFUALTSHELL_HERE USERNAME_HERE` If there are any users that shouldn't be administrators, revoke their privileges and vice-versa using `sudo deluser USERNAME_HERE sudo` and `sudo usermod -aG sudo USERNAME_HERE`, respectively.
  
    2. You can also use usermod -aG to add/remove users from other groups. To create/delete groups use groupadd/groupdel.


6. Application Management

    1. Search for common "hacking-tools" and unwanted software using  `sudo dpkg --get –selections` or `sudo rpm -qa` depending on os. You can also pipe this output into grep to search specific programs (e.g ` sudo dpkg --get –selections | grep APPNAME`). Be sure to look for TelNet, FTP, VNC, NFS, Apache, Samba, etc unless otherwise specified by the readme.
  
    2. Uninstall these packages with `sudo apt-get purge APPNAME`
  
    3. Change startup programs with `sudo systemctl disable SERVICENAME` and `sudo systemctl enable SERVICENAME`
  
    4. Look for programs that automatically start using `sudo nano /etc/init.d/rc.local` and `sudo crontab -e`. Run `sudo apt-get install chkconfig` followed by `sudo chkconfig --list | grep ‘3:on’`  
 


<br><br><br><br><br>

This checklist was formulated from my own knowledge, common knowledge, Cochise College's "Basic Security Checklist – Ubuntu Linux Focus" (https://www.cochise.edu/wp-content/uploads/2021/02/Security-Checklist-Linux.pdf), and bobpaw's "Linux Checklist for Cyberpatriot idk" (https://gist.github.com/bobpaw/a0b6828a5cfa31cfe9007b711a36082f)
