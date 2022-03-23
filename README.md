# Elasticsearch Cluster Installation on Ubuntu 20.04

This is a step by step guide for building elasticsearch cluster on ubuntu 20.04

## Step 1 - Prepare the Environment

Install java11 - You can follow this guideline to install java ([https://github.com/ozgunakin/java-installation-on-ubuntu20.04](https://github.com/ozgunakin/java-installation-on-ubuntu20.04))

Install apt-transport-https

```
sudo apt install apt-transport-https 
```

Update GPG key

```
wget -qO - https://artifacts.elastic.co/GPG-KEY-elasticsearch | sudo apt-key add - 
```

Add the repository to your system

```
add-apt-repository "deb https://artifacts.elastic.co/packages/7.x/apt stable main" 
```

## Step 2 - Install Elasticsearch with Apt

Install latest version ap elasticsearch using apt package manager.

```
sudo apt update 
sudo apt install elasticsearch
```

## Step 3 - Configure Elasticsearch Nodes

You can skip this step if you dont want to access elasticsearch from remote server.

**ON MASTER NODE**

Edit Elasticsearch yml file which is placed in /etc/elasticsearch.

```
sudo nano /etc/elasticsearch/elasticsearch.yml
```

Change/Add the following lines and save the file.

> cluster.name: my-cluster
>
> node.name: master&#x20;
>
> node.master: true&#x20;
>
> node.voting\_only: false&#x20;
>
> node.data: false&#x20;
>
> node.ingest: false&#x20;
>
> node.ml: false
>
>
>
> network.host =0.0.0.0      #sholud be chaged to be able to elastic from remote server
>
> http.port: 9200
>
>
>
> discovery.seed.hosts = \["master-ip-address","datanode1-ip-address","datanode2-ip-address"]
>
> cluster.initial\_master\_nodes: \["master-ip-address"]



**ON DATANODE1**

Edit Elasticsearch yml file which is placed in /etc/elasticsearch.

```
sudo nano /etc/elasticsearch/elasticsearch.yml
```

Change/Add the following lines and save the file.

> cluster.name: my-cluster
>
> node.name: datanode1&#x20;
>
> node.master: false&#x20;
>
> node.voting\_only: false&#x20;
>
> node.data: true&#x20;
>
> node.ingest: true&#x20;
>
> node.ml: false
>
>
>
> network.host =0.0.0.0      #sholud be chaged to be able to elastic from remote server
>
> http.port: 9200
>
>
>
> discovery.seed.hosts = \["master-ip-address","datanode1-ip-address","datanode2-ip-address"]
>
> cluster.initial\_master\_nodes: \["master-ip-address"]



**ON DATANODE2**

Edit Elasticsearch yml file which is placed in /etc/elasticsearch.

```
sudo nano /etc/elasticsearch/elasticsearch.yml
```

Change/Add the following lines and save the file.

> cluster.name: my-cluster
>
> node.name: datanode2
>
> node.master: false&#x20;
>
> node.voting\_only: false&#x20;
>
> node.data: true&#x20;
>
> node.ingest: false&#x20;
>
> node.ml: false
>
>
>
> network.host =0.0.0.0      #sholud be chaged to be able to elastic from remote server
>
> http.port: 9200
>
>
>
> discovery.seed.hosts = \["master-ip-address","datanode1-ip-address","datanode2-ip-address"]
>
> cluster.initial\_master\_nodes: \["master-ip-address"]

## Step 4 - Start & Enable Elasticsearch

!!! HIT THE START CODE ON MASTER FIRST (you can run the code on slaves after 3sec)

Start elasticsearch as a service

```
sudo systemctl start elasticsearch
```

Enable Elasticsearch service

```
sudo systemctl enable elasticsearch
```

Check the status

```
service elasticsearch status
```

