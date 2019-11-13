## Download and install Heartbeat
```
curl -L -O https://artifacts.elastic.co/downloads/beats/heartbeat/heartbeat-7.4.2-amd64.deb
sudo dpkg -i heartbeat-7.4.2-amd64.deb
```

## Configure Heartbeat to monitor the Spring app

Place the file spring-http.yml in /etc/heartbeat/......
```
cd /etc/heartbeat/monitors.d/
sudo curl -L -O https://raw.githubusercontent.com/DanRoscigno/gs-accessing-data-mysql/master/heartbeat/spring.http.yml
```
## Configure Heartbeat

### Keystore

## Metricbeat Keystore
```
sudo heartbeat keystore create

sudo heartbeat keystore add ES_SETUP_USER

# use beat-setup

sudo heartbeat keystore add ES_SETUP_PASSWORD

# example password: C@tf00d

sudo heartbeat keystore add ES_USER

# use beat-writer

sudo heartbeat keystore add ES_USER_PASSWORD

# Another example password C@tf00d
```

## Run Heartbeat setup
```
sudo heartbeat setup \
  -E cloud.id=Observability:dXMtY2VudHJhbDEuZ2NwLmNsb3VkLmVzLmlvJDY4NDI4YWUxMzUzMTRlNjJiMGRhNTZiOWEzYjRhMTBmJDU3YzU5NzM5Y2NmYjQ2ZTRiNWNjMjY2MjIyNzcwYjZj \
  -E cloud.auth=\${ES_SETUP_USER}:\${ES_SETUP_PASSWORD}
```

## Start Heartbeat
```
sudo service heartbeat-elastic start
```
