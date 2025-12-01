# RabbitMQ – Installation & Configuration
RabbitMQ is a message broker supporting AMQP and other protocols.
**Installation (Ubuntu)**
bash
```
sudo apt update
sudo apt install -y rabbitmq-server
sudo systemctl enable --now rabbitmq-server
```
**Configuration**
1. Enable the management UI:
bash
```
sudo rabbitmq-plugins enable rabbitmq_management
```
2. Access:
text
```
http://<rabbitmq-host>:15672
```
3. Create:
•	Virtual hosts
•	Users and permissions
•	Exchanges, queues, and bindings
4. Optionally configure:
•	TLS for secure connections
•	Mirrored / quorum queues for HA
