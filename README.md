#!/bin/bash

yum update -y
yum install java-1.8.0-openjdk -y

wget https://download.elastic.co/elasticsearch/release/org/elasticsearch/distribution/rpm/elasticsearch/2.4.3/elasticsearch-2.4.3.rpm
rpm -ivh elasticsearch-2.4.3.rpm

systemctl daemon-reload

systemctl enable elasticsearch.service
systemctl start elasticsearch.service

cd /opt/
mkdir elasticsearch
chmod 777 elasticsearch/

systemctl status elasticsearch

echo "root hard nofile 200000" | sudo tee -a /etc/security/limits.conf && echo "root soft nofile 200000" | sudo tee -a /etc/security/limits.conf
