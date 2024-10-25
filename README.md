# CyberPatriot-Linux-Checklist
  **Note: Try to do these steps in order as to not prevent yourself from later on**

1. Read The Readme
   
     Note down which ports, users, and protocols are allowed

 
2. **Do Forensics Questions**

     You may destroy the requisite information if you work on the checklist!


3. Updates

     Open a new terminal and run `sudo apt-get update` and `sudo apt-get upgrade`


4. AntiVrius and RootKit Detection

    1. Open a new terminal and run `sudo apt-get install chkrootkit rkhunter`. Then, in order, run `sudo chkrootkit`, `sudo rkhunter --update`, and `sudo rkhunter --check`
    
    2. After that, run `sudo apt-get install clamav`. Then, go to https://gitlab.com/dave_m/clamtk/-/wikis/Downloads and download the appropriate package for your os. Go back to your terminal and install the package with `sudo dpkg -i Downloads/PLACEHOLDER.deb` or `sudo rpm -i Downloads/PLACEHOLDER.deb` as applicable for your os (make sure to replace PLACEHOLDER with the package's filename).
    
    3. Run `sudo freshclam` and `sudo clamscan –i –r --remove=yes /` then minimize this window as it will take over an hour

  
5. User Account Management

    Go to settings>>users and crossreference the users there with the readme. If there are any users that shouldn't be there, check their files for information and then delete them. If there are any users that shouldn't be administrators, revoke their 
   
