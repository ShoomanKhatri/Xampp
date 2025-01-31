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

