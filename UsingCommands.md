# Setting Up PHP and Starting XAMPP Server in Windows

## 1. Set PHP Path in System Environment Variables
To run PHP from any location in Command Prompt, add it to the system PATH.

### **Step 1: Find Your PHP Path**
If you are using XAMPP, the PHP executable is usually located at:
```
C:\xampp\php
```

### **Step 2: Add PHP to System PATH**
1. Press **`Win + R`**, type **`sysdm.cpl`**, and press **Enter**.
2. Go to the **Advanced** tab and click **Environment Variables**.
3. Under **System Variables**, find and select **Path**, then click **Edit**.
4. Click **New**, then enter:
   ```
   C:\xampp\php
   ```
5. Click **OK** on all windows to save changes.

### **Step 3: Verify PHP is Set**
1. Open **Command Prompt (`cmd`)**.
2. Type:
   ```sh
   php -v
   ```
3. If PHP is correctly set, it will display the installed PHP version.

---

## 2. Start XAMPP Apache & MySQL Server from CMD
Once PHP is set, you can start the XAMPP server using CMD.

### **Option 1: Start XAMPP Server**
```sh
cd C:\xampp
xampp_start.exe
```

### **Option 2: Start Apache and MySQL Separately**
```sh
cd C:\xampp
apache_start.bat
mysql_start.bat
```

### **Option 3: Stop the Server (When Needed)**
To stop all services:
```sh
cd C:\xampp
xampp_stop.exe
```
Or stop them individually:
```sh
apache_stop.bat
mysql_stop.bat
```

---

## 3. Run a PHP Server (Optional)
If you want to start a **PHP built-in server**, use:
```sh
php -S 127.0.0.1:8000
```
This will serve PHP files from the current directory at:
```
http://127.0.0.1:8000
```

---

Now you can run PHP commands from anywhere in CMD and start the XAMPP server successfully! 🚀

