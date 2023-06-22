# IP Whitelisting for Maintenance Mode

## Description
This code snippet allows you to put your website into maintenance mode and whitelist specific IP addresses, allowing only those IPs to access the website while it's under maintenance.

## Prerequisites
- Apache web server with `mod_rewrite` enabled

## Installation
1. Open the `.htaccess` file in the root directory of your website.
2. Add the following code snippet to the file:

```apache
RewriteEngine on

# Remote IP from server
RewriteCond %{REMOTE_ADDR} !^45\.152\.46\.105 

# VPN User IP
RewriteCond %{REMOTE_ADDR} !^146\.70\.202\.118

# You can add more IPs from another VPN users like this:
# RewriteCond %{REMOTE_ADDR} !^your\.vpn\.ip\.here

RewriteCond %{REQUEST_URI} !/maintenance.php$ [NC]
RewriteCond %{REQUEST_URI} !\.(jpe?g?|png|gif) [NC]
RewriteRule .* /maintenance.php [R=302,L]
