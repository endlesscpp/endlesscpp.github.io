MicroServices
==============

FileManagerService

Rodger Richard. The Tao of Microservices

## RabbitMQ

### Install

https://www.rabbitmq.com/install-debian.html#apt

### Usage:

sudo service rabbitmq-server start
sudo service rabbitmq-server stop

#### TODO: how to handle the sudo password input during shell script?

ulimit -S -n 65536

/etc/systemd/system/rabbitmq-server.service.d/limits.conf
[Service]
LimitNOFILE=64000


#### manager
https://www.rabbitmq.com/management.html#permissions
sudo rabbitmqctl list_user
sudo rabbitmq-plugins enable rabbitmq_management

// suppose your user name is: janeway
rabbitmqctl add_user_tags <your_user_name>
//rabbitmqctl set_permissions -p my-vhost <your_user_name> "^janeway-.*" ".*" ".*"
rabbitmqctl set_user_tags <your_user_name> administrator

http://127.0.0.1:15672/
by default: user:guest pwd:guest
