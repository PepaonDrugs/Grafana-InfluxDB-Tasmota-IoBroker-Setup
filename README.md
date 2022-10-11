
Setup Guide to setup Grafana, InfluxDB, Tasmota and IoBroker for Powerdraw monitoring
✅
# Install Guides for Grafana-InfluxDB-Tasmota and IoBroker



 # ✅works for Ubuntu, Debian ...✅
 
```bash
sudo su
```

```bash
apt-get update
```

```bash
wget -qO- https://repos.influxdata.com/influxdb.key | sudo apt-key add -
source /etc/os-release
echo "deb https://repos.influxdata.com/debian $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/influxdb.list
sudo apt-get install influxdb
```

```bash
service influxdb start
```

```bash
apt install influxdb-client
```

```bash
influx
```

```bash
CREATE USER "admin" WITH PASSWORD '<admin>' WITH ALL PRIVILEGES
```

```bash
CREATE DATABASE "iobroker"
```

```bash
GRANT ALL ON "iobroker" TO "admin"
```

```bash
exit
```


# configure the Influxdb config

```bash
nano /etc/influxdb/influxdb.conf
```

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
 
```bash
systemctl restart influxdb.service
``` 



#install Grafana

```bash
apt-get install -y gnupg2 curl software-properties-common
curl https://packages.grafana.com/gpg.key | sudo apt-key add -
``` 

```bash
add-apt-repository "deb https://packages.grafana.com/oss/deb stable main"
``` 

```bash
apt-get update
apt-get -y install grafana
``` 

```bash
systemctl enable --now grafana-server
``` 




# Node.js installation

```bash
curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
```

```bash
sudo apt install -y nodejs
```


#IoBroker Installation

```bash
curl -sLf https://iobroker.net/install.sh | bash -
```



# setup influxdb in Grafana 

URL http://your.localip.com:8086 #configer your ip here

Database iobroker
User admin
Password admin


#configure IoBriker
http://your.localip.com:8081/

# Install Influxdb adapter from the instances tab
#configure Influxdb in Iobroker

 |                    |                    |
| ----------------   | ------------------ |
| Server             | your.localip.com   |
| Port               | 8086               |
| Protokoll          | http               |
| User               | admin              |
| Passwort           | •••••••••••        |
| Passwort (repeat)  | •••••••••••        |
| DB Name            | iobroker           |


save and Exit

# Configuer mqtt with Tasmota and Sofnoff

# Tasmota Setup
 |                                 |                    |
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



# Sofnoff Setup 

# Install Sofnoff adapter from the instances tab
#configure Sofnoff in Iobroker


 |                                 |                                      |
| ------------------------------- | ------------------------------------ |
| Verbindungseinstellungen        | [IPv4] 0.0.0.0 - Listen on all IPs   |
| Port                            | 1883                                 |
| Benutzer                        | mqtt                                 |
| Kennwort                        | •••••••                              |
| Password-Wiederholung           | •••••••                              |

 

