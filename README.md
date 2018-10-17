# Installation on Debian Stretch
## NodeRed
`apt-get install nodered`
`sudo systemctl enable nodered.service`

For I2C & InfluxDB modules:
```bash
echo "prefix=/usr" | sudo tee /etc/npmrc
sudo npm install -g node-red-contrib-influxdb node-red-contrib-i2c
sudo service nodered restart
```

## Grafana
```bash
sudo apt-get install apt-transport-https curl
curl https://bintray.com/user/downloadSubjectPublicKey?username=bintray | sudo apt-key add -
echo "deb https://dl.bintray.com/fg2it/deb stretch main" | sudo tee -a /etc/apt/sources.list.d/grafana.list
sudo apt-get update
sudo apt-get install grafana
```

## InfluxDB
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install apt-transport-https
sudo apt-get install curl
curl -sL https://repos.influxdata.com/influxdb.key | sudo apt-key add -
echo "deb https://repos.influxdata.com/debian stretch stable" | sudo tee /etc/apt/sources.list.d/influxdb.list 
sudo apt-get update
sudo apt-get install influxdb
```

# Configuration
## InfluxDB
```bash
influx
create database probes;
create user grafana with password 'grafana' with all privileges;
```

## Grafana
Accessing Grafana (login: admin/admin): http://raspberrypi.local:3000/
Configuration -> Data Sources -> Add data source
- Type: InfluxDB
- HTTP/URL: http://127.0.0.1:8086/
- HTTP/Access: Server (Default)
- InfluxDB Details/Database; User; Password: according to influxDB configuration

## Nodered
Accessing Nodered: http://raspberrypi.local:1880/

# References
https://bentek.fr/influxdb-grafana-raspberry-pi/
