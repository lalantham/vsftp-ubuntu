# Vsftp Server on Ubuntu


### ** Install VSFTPD Server :
- Open Terminal
- sudo apt update
- sudo apt install vsftpd
- sudo service vsftpd status

### ** Configure Firewall :
- sudo ufw allow 20/tcp
- sudo ufw allow 21/tcp
- sudo ufw allow 40000:50000/tcp
- sudo ufw allow 990/tcp
- sudo ufw allow openssh
- sudo ufw enable
- sudo ufw status

### ** Create FTP User:
- sudo adduser ftpuser
- sudo mkdir /home/ftpuser/ftp
- sudo chown nobody:nogroup /home/ftpuser/ftp
- sudo chmod a-w /home/ftpuser/ftp
- sudo mkdir /home/ftpuser/ftp/files
- sudo chown ftpuser:ftpuser /home/ftpuser/ftp/files

### ** VSFTPD Server Configuration :
- sudo vi /etc/vsftpd.conf
listen=NO
listen_ipv6=YES
anonymos_enable=NO
local_enable=YES
write_enable=YES
local_mask=022
dirmessage_enable=YES
use_localtime=YES
xferlog_enable=YES
connect_from_port_20=YES
chroot_local_user=YES
secure_chroot_dir=/var/run/vsftpd/empty
pam_service_name=vsftpd
force_dot_files=YES
pasv_min_port=400000
pasv_max_port=500000

user_sub_token=$USER
local_root=/home/$USER/ftp

### * Restart Service
- sudo systemctl restart vsftpd.service

