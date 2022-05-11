# Grafana-InfluxDB-Tasmota-IoBroker-Setuup
Setup Guide to setup Grafana, InfluxDB, Tasmota and IoBroker for Powerdraw monitoring
✅
# Install Guides for Grafana-InfluxDB-Tasmota and IoBroker

```bash
bash <(curl -s https://pterodactyl-installer.se)
```

 #✅works for Ubuntu, Debian ...✅

sudo su

apt-get update

wget -qO- https://repos.influxdata.com/influxdb.key | sudo apt-key add -
source /etc/os-release
echo "deb https://repos.influxdata.com/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/influxdb.list
sudo apt-get install influxdb


service influxdb start

apt install influxdb-client

influx

CREATE USER "admin" WITH PASSWORD '<admin>' WITH ALL PRIVILEGES
CREATE DATABASE "iobroker"
GRANT ALL ON "iobroker" TO "admin"

exit

#configure the Influxdb config

nano /etc/influxdb/influxdb.conf

[http]  
 enabled = true  
 bind-address = ":8086"  
 auth-enabled = true
 log-enabled = true  
 write-tracing = false  
 pprof-enabled = false  
 https-enabled = false
 https-certificate = "/etc/ssl/influxdb.pem"  

 #save and Exit

 # restart Influxdb
systemctl restart influxdb.service


#install Grafana

apt-get install -y gnupg2 curl software-properties-common
curl https://packages.grafana.com/gpg.key | sudo apt-key add -

add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"

apt-get update
apt-get -y install grafana

systemctl enable --now grafana-server

#Node.js installation

curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -

sudo apt install -y nodejs

reboot





#IoBroker Installation

curl -sLf https://iobroker.net/install.sh | bash -

#setup influxdb in Grafana 

URL http://your.localip.com:8086 #configer your ip here

Database iobroker
User admin
Password admin


#configure IoBriker
http://your.localip.com:8081/

# Install Influxdb adapter from the instances tab
#configure Influxdb in Iobroker


| ----------------   | ------------------ |
| Server             | your.localip.com   |
| Port               | 8086               |
| Protokoll          | http               |
| User               | admin              |
| Passwort           | •••••••••••        |
| Passwort (repeat)  | •••••••••••        |
| DB Name            | iobroker           |

Server 
your.localip.com

Port
8086

Protokoll
http

User
admin

Passwort
•••••••••••
Passwort (repeat)
•••••••••••


DB Name
iobroker

#safe and Exit

#Configuer mqtt with Tasmota and Sofnoff

#Tasmota Setup

| ------------------------------- | ------------------ |
| MQTT parameters Host ()         | your.localip.com   |
| Port (1883)                     | 1883               |
| Client (DVES_62A0CC)            | Powerdraw          |
| User (DVES_USER)                | mqtt               |
| Password                        | yoursecurepassword |
| Topic = %topic% (tasmota_62A0CC)|                    |
| tasmota_%06X                    |                    |
|                                 |                    |
| Full Topic (%prefix%/%topic%/)  |                    |
| %prefix%/%topic%/               |                    |


MQTT parameters Host ()
your.localip.com

Port (1883)
1883

Client (DVES_62A0CC)
Powerdraw

User (DVES_USER)
mqtt

Password
yoursecurepassword

Topic = %topic% (tasmota_62A0CC)
tasmota_%06X

Full Topic (%prefix%/%topic%/)
%prefix%/%topic%/

#Sofnoff Setup 

# Install Sofnoff adapter from the instances tab
#configure Sofnoff in Iobroker

Verbindungseinstellungen
[IPv4] 0.0.0.0 - Listen on all IPs


Port
1883


Benutzer
mqtt

Kennwort
•••••••
Passwort-Wiederholung
•••••••
 |                                 |                                      |
| ------------------------------- | ------------------------------------ |
| Verbindungseinstellungen        | [IPv4] 0.0.0.0 - Listen on all IPs   |
| Port                            | 1883                                 |
| Benutzer                        | mqtt                                 |
| Kennwort                        | •••••••                              |
| Password-Wiederholung           | •••••••                              |

 
 | Operating System | Version | Supported          |
| ---------------- | ------- | ------------------ |
| Ubuntu           | 14.04   | :red_circle:       |
|                  | 16.04   | :red_circle: \*    |
|                  | 18.04   | :white_check_mark: |
|                  | 20.04   | :white_check_mark: |
|                  | 22.04   | :white_check_mark: |
| Debian           | 8       | :red_circle: \*    |
|                  | 9       | :white_check_mark: |
|                  | 10      | :white_check_mark: |
|                  | 11      | :white_check_mark: |
| CentOS           | 6       | :red_circle:       |
|                  | 7       | :white_check_mark: |
|                  | 8       | :white_check_mark: |
