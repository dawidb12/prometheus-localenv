# Prometheus Local Environment

## Instructions
1. Make sure Vagrant is installed.
2. Clone the repository and run the command `vagrant up`
3. Log into all newly created nodes. Their IP addresses are as follows:

| hostname          | ip address     | 
|-------------------|----------------|
| prometheus-server | 192.168.56.101 |
| server1           | 192.168.56.102 |
| server2           | 192.168.56.103 |

4. Go to directory /vagrant/prometheus_node_cadvisor
5. On prometheus-server run the command `docker-compose up -d`
6. On server1 and server2 run the command `docker-compose -f docker-compose.exporters.yml up -d`
7. Open your web browser and navigate to: http://192.168.56.101:9090/
8. If you want to experiment with Grafana, enter: http://192.168.56.101:3000/

## Known issues
```
Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get http://%2Fvar%2Frun%2Fdocker.sock/v1.40/containers/json: dial unix /var/run/docker.sock: connect: permission denied
```
1. Make sure the vagrant user is in 'docker' group
2. Run the command `sudo chmod 666 /var/run/docker.sock`
