# 2420_week11_Lab

## Authors
  - Braeden Venne
  - Gurshawn Sekhon

## Installation
Clone the repository using

    git clone https://github.com/BraedenVenne/2420_week11_Lab.git
  
  Example output
  ![picture of installation output](/images/installation.PNG)

## Backup Service

The backup service will backup a specific directory to a backup server every Friday at 01:00

### backup.conf
  1. Create a **backup.conf** file with a text editor
  
    vim backup.conf
 
  The backup.conf file should contain the following:

  ![picture of backup.conf](/images/backup-conf.PNG)

  2. Set the **DIR** variable to the path of the directory or directories you want to backup

  3. Set the **IP** variable to the user and IP of your backup-server 
  i.e. [backup-server-username]@[backup-server-IP]

  4. Set the **KEY** variable to the backup-server key filename
  
  5. Put backup.conf in **/etc**

    sudo cp backup.conf /etc

  ### backup-script
  1. Create a directory in **/opt** to store the backup-script
  
    sudo mkdir /opt/backup
  
  2. Give **backup-script** execute permissions

    chmod +x backup-script

  3. Put **backup-script** in the new directory  
    
    sudo cp backup-script /opt/backup/

  ### backup.service
  1. Put **backup.service** in the **/etc/systemd/system**

    sudo cp backup.service /etc/systemd/system
 
  ### backup.timer 
  1. Set the timezone to PST
    
    sudo timedatectl set-timezone America/Vancouver

  2. Check if timezone is correct
    
    timedatectl
   
   Example output
   ![picture of current timezone](/images/timezone.PNG)

  3. Put **backup.timer** in the **/etc/systemd/system**

    sudo cp backup.timer /etc/systemd/system

  ### Starting/Reloading the service
  1. Reload the service

    sudo systemctl daemon-reload

  2. Start **backup.service**

    sudo systemctl start backup.service

  3. Check the status of **backup.service**
  
    systemctl status backup.service
    
    Output should be as follows
    ![picture of backup.service status](/images/status.PNG)

  4. Enable **backup.service**

    sudo systemctl enable --now backup.service
    
  5. Enable **backup.timer** 
    
    sudo systemctl enable --now backup.timer

  6. Check if **backup.timer** is active 

    sytemctl list-timers

  backup.timer should be displayed in the list of timers
  ![picture of active timers](/images/checktimer.png)
  
  ### Output of the Backup Service
  output should be as follows
  ![picture of the output](/images/output.PNG)
