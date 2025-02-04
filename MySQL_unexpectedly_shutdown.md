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

