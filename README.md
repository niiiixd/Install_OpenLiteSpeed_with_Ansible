# Install OpenLightSpeed with Ansible

OpenLiteSpeed is an open-source HTTP server developed by LiteSpeed Technologies. It is a high-performance and lightweight HTTP server with a web-based GUI for administration.
OpenLiteSpeed can handle more than a hundred thousand concurrent connections with low resource consumption (CPU and RAM) and supports many operating systems such as Linux, Mac OS, FreeBSD, and SunOS. The server can be used to run web page scripts written in PHP, Ruby, Perl, and Java.

With this playbook, we will install OpenLiteSpeed with the MariaDB database and PHP 7.4 on the CentOS 8 server.

### Prerequisites

we will be using the latest CentOS 8 server with 2GB of RAM, 25GB free disk space, and 2 CPUs.

Install OpenLightSpeed with Ansible Playbook - run the playbook as root The option `--become` is required, as for example installing packages and interacting with various systemd daemons.
Without --become the playbook will fail to run!

``` ansible-playbook -i inventory/hosts.yaml  --become --become-user=root litespeed.yaml ```

## Admin Authentication
OpenLiteSpeed provides a web-based dashboard for managing its configuration.

In this step, we will open port '7080' on the firewalld rules and set up the user and password authentication for the OpenLiteSpeed dashboard.
By default, the openlitespeed dashboard is running on port '7080'. And we will add the port '7080' to the firewalld.
Add port '7080' to the firewalld rules and reload the service using the 'firewall-cmd' command below.

```
firewall-cmd --add-port=7080/tcp --permanent
firewall-cmd --reload

```
Next, we will set up the OpenLitespeed dashboard authentication.
Go to the '/usr/local/lsws/admin/misc' directory and run the 'admpass.sh' script.

```
cd /usr/local/lsws/admin/misc
sh admpass.sh
```
Type your admin user and password, and you've set up the authentication for the OpenLitespeed admin dashboard.

Now open your web browser and type the server IP address followed by the port '7080' on the address bar.

``` https://192.168.122.163:7080/ ```

Log in with your user and password.

