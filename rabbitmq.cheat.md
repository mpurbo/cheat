# RabbitMQ Cheat Sheet

## Installation

Installing Erlang and RabbitMQ on AWS EC2 Amazon Linux:
```bash
sudo yum install erlang

wget http://www.rabbitmq.com/releases/rabbitmq-server/v3.2.1/rabbitmq-server-3.2.1-1.noarch.rpm
sudo rpm --import http://www.rabbitmq.com/rabbitmq-signing-key-public.asc
sudo yum install rabbitmq-server-3.2.1-1.noarch.rpm
```

On OSX, use `brew` to install:
```bash
brew install rabbitmq
```

## Starting and stopping

To start RabbitMQ as daemon on reboot:
```bash
sudo chkconfig rabbitmq-server on
```

To start and stop RabbitMQ manually:
```bash
sudo service rabbitmq-server start
sudo service rabbitmq-server stop
```

Starting the server on OSX:
```bash
rabbitmq-server
# so that the server runs in background
rabbitmq-server -detached
```

To stop the server on OSX:
```bash
rabbitmqctl stop
```

## Basic queue management

Restarting RabbitMQ will not remove persistent queues, etc. To reset and clean up everything (queues, vhosts, users), do:
```bash
rabbitmqctl stop_app
rabbitmqctl reset
rabbitmqctl start_app
```
