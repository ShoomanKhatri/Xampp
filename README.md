- [Fix MySQL Access Denied & Port Issues](#fix-mysql-access-denied--port-issues)
- [XAMPP Apache Port 80 Error](#xampp-apache-port-80-error)
- [How to Fix MySQL Unexpected Shutdown Error in XAMPP](#how-to-fix-mysql-unexpected-shutdown-error-in-xampp)



# Fix MySQL Access Denied & Port Issues

## 1. Check MySQL Service Status
- **Windows (XAMPP):** Open XAMPP and start MySQL.
- **Linux/macOS:** Run:
  ```sh
  sudo systemctl start mysql  # or mariadb
  ```

## 2. Change MySQL Port (If Needed)
- Open `my.ini` (Windows) or `my.cnf` (Linux/macOS).
- Find:
  ```ini
  port=3306
  ```
- Change it to `3307` (or any available port):
  ```ini
  port=3307
  ```
- Restart MySQL.
- Update `config.inc.php`:
  ```php
  $cfg['Servers'][$i]['host'] = '127.0.0.1';
  $cfg['Servers'][$i]['port'] = '3307';
  ```

## 3. Fix MySQL Access Denied
### a) Reset Root Password
1. Stop MySQL:
   ```sh
   sudo systemctl stop mysql
   ```
2. Start MySQL in safe mode:
   ```sh
   sudo mysqld_safe --skip-grant-tables --skip-networking &
   ```
3. Open MySQL:
   ```sh
   mysql -u root
   ```
4. Reset password:
   ```sql
   ALTER USER 'root'@'localhost' IDENTIFIED BY 'newpassword';
   FLUSH PRIVILEGES;
   ```
5. Restart MySQL:
   ```sh
   sudo systemctl restart mysql
   ```

### b) Update `config.inc.php`
- If MySQL has a password:
  ```php
  $cfg['Servers'][$i]['user'] = 'root';
  $cfg['Servers'][$i]['password'] = 'newpassword';
  ```

## 4. Allow Root Login Without Password (Optional)
- Change `config.inc.php`:
  ```php
  $cfg['Servers'][$i]['AllowNoPassword'] = true;
  ```
- Add in `my.cnf`:
  ```ini
  skip-grant-tables
  ```
- Restart MySQL.

## 5. Check Firewall & Open MySQL Port
- Check if MySQL port is open:
  ```sh
  netstat -tulnp | grep 3306
  ```
- Allow MySQL port:
  ```sh
  sudo ufw allow 3306/tcp
  ```

## 6. Restart Services
- Restart MySQL & Apache.
- Try accessing **phpMyAdmin** again.

### ✅ Issue should be resolved! 🚀

---


### XAMPP Apache Port 80 Error

**Issue:**
- Apache fails to start due to Port 80 being already in use by another process with PID 4.
  
**Solution:**
1. **Identify Blocking Application:**
   - Port 80 is commonly used by services like Skype, IIS, or other applications.
   - Open **Task Manager** and look for the process with PID 4. This might be the system's HTTP service or another application using Port 80.

2. **Disable or Reconfigure the Blocking Application:**
   - **Skype:** Go to Skype settings > Advanced > Connection and uncheck "Use port 80 and 443 for incoming connections."
   - **IIS (Internet Information Services):** Disable IIS or stop the World Wide Web Publishing Service from the **Services** tab.

3. **Reconfigure Apache to Use a Different Port:**
   - Open the **httpd.conf** file in the XAMPP directory (`C:\xampp\apache\conf\httpd.conf`).
   - Change the line `Listen 80` to `Listen 8080` (or any other available port).
   - Change the line    `ServerName localhost:80` to `ServerName localhost:8080`.
   - Save and restart Apache.

**Note:** If you change the port, remember to update the XAMPP Control Panel and your browser's URL to `http://localhost:8080` (or your chosen port).

---

This should resolve the conflict and allow Apache to start successfully.

# **How to Fix MySQL Unexpected Shutdown Error in XAMPP**

## **Overview**
If MySQL in XAMPP unexpectedly shuts down, it may be due to corruption in database files. The following steps will guide you through resolving this issue by preserving essential files and restoring backups.

---

## **Step-by-Step Guide**

### **Step 1: Navigate to the MySQL Data Folder**
1. Open the XAMPP installation directory.
2. Go to the `mysql` folder.
3. Inside `mysql`, open the `data` folder.

**Path:** `xampp/mysql/data`

### **Step 2: Keep Essential Files and Delete Others**
1. Locate the file **`ibdata1`** – this is essential, do not delete it.
2. Identify the database folders that you need and keep them (each database has its own folder).
3. Delete all other remaining files and folders inside the `data` folder.

### **Step 3: Restore Backup Data**
1. Open the `backup` folder located inside `mysql`.
2. Copy all contents from the `backup` folder.
3. Paste them into the `data` folder.

### **Step 4: Restart MySQL**
1. Open **XAMPP Control Panel**.
2. Click **Start** next to MySQL.
3. MySQL should now run without issues.

---

## **Conclusion**
By following these steps, you can fix the MySQL shutdown error efficiently. This process ensures that essential database files are retained while replacing potentially corrupted files with backups.

🔹 **Tip:** Always maintain regular backups of your MySQL databases to prevent data loss and make recovery easier.

---
✅ **Problem Solved!** 🚀


