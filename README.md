# vagrant-big-data

Vagrantfiles for development in big data

# Install

git clone this project to your local computer and cd to one of the directory, then run "vagrant up".

# Usage

### Zookeeper Cluster

cd to the directory "zookeeper" under the root directory and run "vagrant up". This will study a multi-machine vagrant 
setup in which three ubuntu VMs runs a zookeeper cluster. The three ubuntu VMs have the following ip address 
by default (hostname:ip-address):

* zoo1: 192.168.10.12
* zoo2: 192.168.10.13
* zoo3: 192.168.10.14

To login to one of the VMs, say zoo1, run "vagrant ssh zoo1".

To check the status of the zookeeper cluster, run the following command (e.g., from within the zoo1 VM):

```bash
echo stat | nc zoo1 2181
echo stat | nc zoo2 2181
echo stat | nc zoo3 2181
```

The log of the zookeeper is located in the VMs at "/var/log/zookeeper/zookeeper.log"
The zoo.cfg for configuration is located in the VMs at "/etc/zookeeper/conf/zoo.cfg"

Run "vagrant suspend" or "vagrant resume" to stop or restart the zookeeper cluster.

### Zookeeper+Kafka Cluster

cd to the directory "zookeeper+kafka" under the root directory and run "vagrant up". This will study a multi-machine vagrant 
setup in which three ubuntu VMs runs a zookeeper cluster. The three ubuntu VMs have the following ip address 
by default (hostname:ip-address):

* zoo1: 192.168.10.12
* zoo2: 192.168.10.13
* zoo3: 192.168.10.14
* kafka1: 192.168.10.15

To login to one of the VMs, say kafka1, run "vagrant ssh kafka1".

For the zookeeper configuration, refers to the earlier section.

For the kafka1, the installation directory is in /opt/kafka,the configuration server.properties can be found in /opt/kafka

To test the kafka producer, create a topic and send a message to the topic using the following command in kafka1:

```bash
echo "Hello, World" | /opt/kafka/bin/kafka-console-producer.sh --broker-list kafka1:9092 --topic TutorialTopic > /dev/null
```

To test the kafka consumer, run the following command:

```bash 
/opt/kafka/bin/kafka-console-consumer.sh --zookeeper localhost:2181 --topic TutorialTopic --from-beginning
```

