# Change welcome.conf
mv /etc/httpd/conf.d/welcome.conf /etc/httpd/conf.d/welcome.backup

# Restart Apache
systemctl restart httpd
