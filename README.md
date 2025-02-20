# Installing and Configuring vsftpd on Ubuntu

This guide provides step-by-step instructions to install, configure, and set up **vsftpd** on Ubuntu with full access to the FTP home directory.

## **1. Update System and Install vsftpd**
First, update the package list and install **vsftpd**:

```bash
sudo apt update
sudo apt install vsftpd -y
```

## **2. Configure vsftpd**
Open the **vsftpd** configuration file and modify the settings:

```bash
sudo nano /etc/vsftpd.conf
```

Replace the content with the following configuration:

```ini
listen=YES
listen_ipv6=NO
ssl_enable=NO
local_enable=YES
write_enable=YES
chroot_local_user=YES
allow_writeable_chroot=YES
user_sub_token=$USER
local_root=/home/$USER
```

Save and close the file (`Ctrl + X`, then `Y`, and `Enter`).

## **3. Create FTP User and Set Permissions**
Create a new FTP user:

```bash
sudo adduser set-ftp
```

Set the home directory for the FTP user:

```bash
sudo usermod -d /home/set-ftp set-ftp
```

Adjust directory permissions to allow full access:

```bash
sudo chmod -R 755 /home/set-ftp
sudo chown -R set-ftp:set-ftp /home/set-ftp
```

## **4. Restart vsftpd Service**
After making the changes, restart the **vsftpd** service:

```bash
sudo systemctl restart vsftpd
```

Check the service status to ensure it's running properly:

```bash
sudo systemctl status vsftpd
```

## **5. Connect to FTP Server**
Use an FTP client (e.g., FileZilla) and connect with:
- **Host:** `ftp://your-server-ip`
- **Username:** `set-ftp`
- **Password:** (the one you set during user creation)

Now, your FTP server is up and running! 🚀

