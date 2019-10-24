# Clean-up yum
yum clean all
# Update Software Versions List
yum update
# Install Apache
yum install httpd
# Activate Apache
systemctl start httpd
# set the Apache service to start when the system boots
systemctl enable httpd
# Verify Apache Service
systemctl status httpd

# Configure firewalld to Allow Apache Traffic
sudo firewall-cmd ––permanent ––add-port=80/tcp
sudo firewall-cmd ––permanent ––add-port=443/tcp
# reload the firewall
sudo firewall-cmd ––reload

# Configure Virtual Hosts on CentOS 7 (optional)
Virtual hosts are different websites that you run from the same server. Each website needs its own configuration file.

Make sure these configuration files use the .conf extension, and save them in the /etc/httpd/conf.d/ directory.

There are a couple of best practices to use when you’re setting up different websites on the same server:

Try to use the same naming convention for all your websites.
For example:
/etc/httpd/conf.d/MyWebsite.com.conf
/etc/httpd/conf.d/TestWebsite.com.conf
Use a different configuration file for each domain. The configuration file is called a vhost, for a virtual host. You can use as many as you need. Keeping them separate makes troubleshooting easier.
1. To create a virtual host configuration file, enter the following into a terminal window:

sudo vi /etc/httpd/conf.d/vhost.conf
This will launch the Vi text editor, and create a new vhost.conf file in the /etc/httpd/conf.d directory.

2. In the editor, enter the following text:

NameVirtualHost *:80

<VirtualHost *:80>

ServerAdmin webmaster@MyWebsite.com

ServerName MyWebsite.com

ServerAlias www.MyWebsite.com

DocumentRoot /var/www/html/MyWebsite.com/public_html/

ErrorLog /var/www/html/MyWebsite.com/logs/error.log

CustomLog /var/www/html/MyWebsite.com/logs/access.log combined

.  </VirtualHost>
Save the file and exit.

3. Next, enter the following command to create a directory for you to store your website files in:

sudo mkdir /var/www/MyWebsite/{public_html, logs}
4. Restart the Apache service to apply your changes by entering:

sudo systemctl restart httpd
Once the system finishes, you should be able to open a browser window to MyWebsite.com and see a default Apache test page.

You can replace MyWebsite above with the name of your domain. If you are hosting more than one domain, make sure you create a new directory in /var/www/ for each one. You can copy the code block in your /etc/httpd/conf.d/vhost.conf file, and replace MyWebsite with another domain name that you’re hosting.

Apache Directories and Files
One of the main ways Apache functions is through configuration files. They are located at /etc/httpd.

Apache has a main configuration file: /etc/httpd/conf/httpd.conf .

If there are any other configuration files, they are included in the main configuration file. They should use the .conf extension and should be stored in the /etc/httpd/conf.d/ directory.

You can enhance Apache’s functionality by loading additional modules.

The configuration files for these modules should be stored in: /etc/httpd/conf.modules.d/ directory.

Log files record all the activity of the Apache service, including client activity on the websites your system is hosting. These logs can be found in:  /var/log/httpd/.

Commands For Managing Apache Service
Other commands that you can use to control the Apache service include:

Stop Apache Service:

sudo systemctl stop httpd
Prevent or disable Apache from starting when the system boots:

sudo systemctl disable httpd
Re-enable Apache at boot:

sudo systemctl enable httpd
Restart Apache and apply any changes you have made:

sudo systemctl restart httpd
