# MariaDB 10.2 Two Node Galera Cluster Experiment
###  2 Galera Nodes, 2 MaxScale Nodes (Using Galera Arbitrator To Avoid Split Brain)

In this experiment I am going to test the stability of using a two node Galera cluster and an arbitrator to create a quorum. The hope is that we can reduce the overall cost of a typical HA Galera cluster by 20%.

#### Prerequisites

* [Git](https://git-scm.com/download/)
* [Vagrant 2.0.0+](https://www.vagrantup.com/downloads.html)
* [Virtualbox 5.1+](https://www.virtualbox.org/wiki/Downloads)
* Ansible
  * [Ansible 2.4+ For MacOS/Linux](http://docs.ansible.com/ansible/latest/intro_installation.html) 
  * [Ansible 2.4+ For Windows](https://www.jeffgeerling.com/blog/2017/using-ansible-through-windows-10s-subsystem-linux)

#### Setup

* `git clone https://github.com/toddstoffel/galera_arbitrator_project.git`
* cd to cloned folder
* `vagrant plugin install vagrant-vbguest`
* `vagrant up`
* `ansible-playbook -i hosts galera.yml`

#### MariaDB Node Access

* `vagrant ssh node1` or `vagrant ssh node2`

#### MaxScale Node Access

* `vagrant ssh node3` or `vagrant ssh node4`

#### Verify Cluster Size (2 Galera & 1 Arbitrator)

`MariaDB [(none)]> SHOW STATUS LIKE 'wsrep_cluster_size';`

* Demo User: **dba**
* Demo Pass: **demo_password**

#### Test Arbitrator Failover

Shutting down node 3 (simulated failure) should cause an automatic failover of the Galera arbitrator to node 4 while maintaining a cluster quorum.

#### Avoiding Single Point of Failure

MariaDB Connector/J supports server failover. The failover is configured at the initial setup stage of the server connection by the connection URL (see explanations for its format [here](https://mariadb.com/kb/en/library/about-mariadb-connector-j/)).

The format of the JDBC connection string is:
> jdbc:(mysql|mariadb):[replication:|failover:|sequential:|aurora:]//<hostDescription>[,<hostDescription>...]/[database][?<key1>=<value1>[&<key2>=<value2>]]

HostDescription:
> <host>[:<portnumber>]  or address=(host=<host>)[(port=<portnumber>)][(type=(master|slave))]

Additional information may be found [here](https://dev.mysql.com/doc/connector-j/5.1/en/connector-j-config-failover.html).

####  Clean Up Project

* `vagrant destroy --force`

#### Additional Notes:

While not important for this demonstration, please open the following ports between nodes when moving this project to real servers:

* **3306** For MySQL client connections and State Snapshot Transfer that use the mysqldump method.
* **4567** For Galera Cluster replication traffic, multicast replication uses both **UDP** transport and **TCP** on this port.
* **4568** For Incremental State Transfer.
* **4444** For State Snapshot Transfer.

#### Need Additional Help?

* Consulting: https://mariadb.com/services/consulting
* Enterprise Architect: https://mariadb.com/services/enterprise-architect
