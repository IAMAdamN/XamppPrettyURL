
## XamppPrettyURL - Xampp Pretty URL Guide With SSL/HTTPS
## **[NatadTech.com](https://natadtech.com)**
## **For Windows**

**Step 1: Edit Hosts File**

1. Open Notepad as administrator. `Run as administrator`
2. Go to `C:\Windows\System32\drivers\etc\hosts`.
3. Open the `hosts` file.
4. Add the following line at the end of the file:```127.0.0.1   project1.web ```
5. Save the file.

**Step 2: Create SSL Certificate**

1. Open Command Prompt as administrator. (Search for Command Prompt, right-click, and select "Run as administrator")
2. Navigate to the XAMPP SSL directory by running:

   ```
   cd C:\xampp\apache\bin
   ```

3. Generate a self-signed SSL certificate:

   ```
   openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout project1.web.key -out project1.web.crt
   ```

   Follow the prompts to fill in the certificate information.

**Step 3: Configure Virtual Host**

1. Navigate to the Apache configuration directory:

   ```
   cd C:\xampp\apache\conf\extra
   ```

2. Open the `httpd-vhosts.conf` file in a text editor.

3. Add the following configuration:

   ```
   <VirtualHost *:80>
       ServerName project1.web
       DocumentRoot "C:/xampp/htdocs/your_project"
       <Directory "C:/xampp/htdocs/your_project">
           Options Indexes FollowSymLinks
           AllowOverride All
           Require all granted
       </Directory>
   </VirtualHost>

   <VirtualHost *:443>
       ServerName project1.web
       DocumentRoot "C:/xampp/htdocs/your_project"
       <Directory "C:/xampp/htdocs/your_project">
           Options Indexes FollowSymLinks
           AllowOverride All
           Require all granted
       </Directory>

       SSLEngine on
       SSLCertificateFile "C:/xampp/apache/conf/ssl/project1.web.crt"
       SSLCertificateKeyFile "C:/xampp/apache/conf/ssl/project1.web.key"
   </VirtualHost>
   ```

   Replace `"C:/xampp/htdocs/your_project"` with the actual path to your project.

**Step 4: Restart Apache**

1. Save the file and close the text editor.
2. Restart Apache from the XAMPP Control Panel.

**Step 5: Test**

You should now be able to access your project using the URL `https://project1.web` in your browser.

##
## **For MAC**

**Step 1: Edit Hosts File**

1. Open Terminal.

2. Open the hosts file by running:

   ```
   sudo nano /etc/hosts
   ```

3. Add the following line at the end of the file:

   ```
   127.0.0.1   project1.web
   ```

   Save the file by pressing `Ctrl + O`, then press `Enter`, and exit by pressing `Ctrl + X`.

**Step 2: Create SSL Certificate**

1. Open Terminal.

2. Navigate to the Apache SSL directory:

   ```
   cd /Applications/XAMPP/xamppfiles/etc/ssl
   ```

3. Generate a self-signed SSL certificate:

   ```
   sudo openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout project1.web.key -out project1.web.crt
   ```

   Follow the prompts to fill in the certificate information.

**Step 3: Configure Virtual Host**

1. Open Terminal.

2. Navigate to the Apache configuration directory:

   ```
   cd /Applications/XAMPP/xamppfiles/etc/extra
   ```

3. Create a new virtual host configuration file:

   ```
   sudo nano project1.web.conf
   ```

4. Add the following configuration:

   ```
   <VirtualHost *:80>
       ServerName project1.web
       DocumentRoot "/Applications/XAMPP/htdocs/your_project"
       <Directory "/Applications/XAMPP/htdocs/your_project">
           Options Indexes FollowSymLinks
           AllowOverride All
           Require all granted
       </Directory>
   </VirtualHost>

   <VirtualHost *:443>
       ServerName project1.web
       DocumentRoot "/Applications/XAMPP/htdocs/your_project"
       <Directory "/Applications/XAMPP/htdocs/your_project">
           Options Indexes FollowSymLinks
           AllowOverride All
           Require all granted
       </Directory>

       SSLEngine on
       SSLCertificateFile "/Applications/XAMPP/xamppfiles/etc/ssl/project1.web.crt"
       SSLCertificateKeyFile "/Applications/XAMPP/xamppfiles/etc/ssl/project1.web.key"
   </VirtualHost>
   ```

   Replace `"/Applications/XAMPP/htdocs/your_project"` with the actual path to your project.

**Step 4: Enable Virtual Host**

1. Open Terminal.

2. Open the Apache configuration file `httpd.conf`:

   ```
   sudo nano /Applications/XAMPP/xamppfiles/etc/httpd.conf
   ```

3. Uncomment the line:

   ```
   Include etc/extra/httpd-vhosts.conf
   ```

**Step 5: Restart Apache**

1. Save the file and exit the editor.

2. Restart Apache from XAMPP control panel.

**Step 6: Test**

You should now be able to access your project using the URL `https://project1.web` in your browser.

##
## **Note:**
##### Specifying the Open SSL Configuration File when generating.
##### Example
````
openssl req -x509 -nodes -days 365 -newkey rsa:2048 -keyout project1.web.key -out project1.web.crt -config "D:\laragon\bin\apache\httpd-2.4.58-240131-win64-VS17\conf\openssl.cnf"
````

##### XAMPP
On the XAMPP installations, the openssl.cnf file usually can be found here:
``C:\xampplite\apache\conf\openssl.cnf``

If you dont have your XAMPP installed on the C drive, just edit the beginning of the path. In some cases, Apache version number is included in the path too, for example:
``D:\xampplite\apache2.4.9\conf\openssl.cnf``

##### WAMP
On the WAMP installations, the openssl.cnf file usually can be found here:
``C:\wamp\bin\apache2.4.9\conf\openssl.cnf``

##### MAMP
On the MAMP installations, the openssl.cnf file usually can be found here:
``C:\MAMP\bin\apache\conf\openssl.cnf``

##### Laragon
On the Laragon installations, the openssl.cnf file usually can be found here:
``C:\laragon\bin\apache\httpd-2.4.47-win64-VS16*\conf\openssl.cnf``

