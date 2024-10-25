# CyberPatriot-Linux-Checklist

  **Note: Try to do these steps in order as to not prevent yourself from later on**


## Main Checklist


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

    1. Run `sudo getent passwd` cross-reference the users listed with the readme. If there are any users that shouldn't be there, check their files for information and then delete them using `sudo userdel --remove-home USERNAME_HERE` (**do not delete system users!!!*).
      
    2. To create a user, use `useradd -u UID_HERE -d HOMEDIR_HERE -s DEFUALTSHELL_HERE USERNAME_HERE`.
  
    3. Change a user's password or add one with `sudo passwd USERNAME_HERE`. Then, enter the new password.
   
    4. If there are any users that shouldn't be administrators, revoke their privileges and vice-versa using `sudo deluser USERNAME_HERE sudo` and `sudo usermod -aG sudo USERNAME_HERE`, respectively. (You can also use usermod -aG to add/remove users from other groups)
      
    5. To create/delete groups use groupadd/groupdel.


6. Application Management

    1. Search for common "hacking-tools" and unwanted software using  `sudo dpkg --get –selections` or `sudo rpm -qa` depending on os. You can also pipe this output into grep to search specific programs (e.g ` sudo dpkg --get –selections | grep APPNAME`). Be sure to look for TelNet, FTP, VNC, NFS, Apache, Samba, etc unless otherwise specified by the readme.
  
    2. Uninstall these packages with `sudo apt-get purge APPNAME`
  
    3. Change startup programs with `sudo systemctl disable SERVICENAME` and `sudo systemctl enable SERVICENAME`
  
    4. Look for programs that automatically start using `sudo nano /etc/init.d/rc.local` and `sudo crontab -e`. Run `sudo apt-get install chkconfig` followed by `sudo chkconfig --list | grep ‘3:on’`


7. Firewall

    1. Check the firewall's status with `sudo ufw status` and, if needed, enable the firewall with `sudo ufw enable`
   
    2. Install the GUI for the native firewall using `sudo apt-get gufw`. Then open the application and set everything to incoming: allow, outgoing: deny.
  
    3. Make a rule to let CyberPatriot systems through the firewall using `sudo ufw allow from IP_HERE`
  
    4. Look for suspicious rules with `sudo ufw status numbered verbose` and delete them with `sudo ufw delete NUMBER_HERE`
  
    5. Activate TCP SYN cookie protection using `sudo nano /etc/sysctl.conf`, changing the value of "net.ipv4.tcp_syncookies" to 1 

  
9. Password Settings

    1. Change password age settings with `sudo nano /etc/login.defs` and save.
  
        * Change PASS_MAX_DAYS to 30
      
        * Change PASS_MIN_DAYS to 10
      
        * Change PASS_WARN_AGE to 7

    2. Install cracklib with `sudo apt-get install libpam-crackib` and run `sudo nano /etc/pam.d/common-auth`. Add the line "auth required pam_tally2.so deny=5 onerr=fail unlocktime=1800" to the end of the file and save.
  
    3. Change password complexity with `sudo nano /etc/pam.d/common-password`. Add "remember=5 minlen=8 difok=3 minclass=4" after pam_unix.so and add the line "password required pam_cracklib.so ucredit=-1 lcredit=-1 dcredit=-1 ocredit=-1" below the former line.
  

  
 
 
## Miscellaneous

1. 



<br><br><br><br><be>

## Attribution
This checklist was formulated from my own knowledge, common knowledge, Cochise College's "Basic Security Checklist – Ubuntu Linux Focus" (https://www.cochise.edu/wp-content/uploads/2021/02/Security-Checklist-Linux.pdf), and bobpaw's "Linux Checklist for Cyberpatriot idk" (https://gist.github.com/bobpaw/a0b6828a5cfa31cfe9007b711a36082f)
