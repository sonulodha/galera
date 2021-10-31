
# Galera Cluster
    Install MariaDB Galera Cluster on Linux
    The Scenario

    The You are working as a Systems Administrator in a large company with many distributed offices, and have been tasked 
    with setting up a MySQL-compatible cluster. You have chosen to implement MariaDB Galera cluster as a proof of concept.
 
# In order to do this, you will need to complete the following tasks.
    1. Install the packages.
    2. Configure the firewall and SELinux.
    3. Bootstrap a new cluster.
    4. Add nodes to the cluster.



The YUM repository file and node configurations are available in the download section of this course.
Logging In

Log into each of the nodes as ec2-user.
Install the Packages

On node1, create the MariaDB.repo file:
[node1 ]$ sudo su - 
no
[node1 ]# cd /etc/yum.repos.d/
cat <<EOF > MariaDB.repo
#http://downloads.mariadb.org/mariadb/repositories/
[mariadb]
name = MariaDB
baseurl = http://yum.mariadb.org/10.4/centos7-amd64
gpgkey=https://yum.mariadb.org/RPM-GPG-KEY-MariaDB
gpgcheck=1
EOF
  
[node1 ]# yum repolist 
[node1 ]# yum -y install MariaDB-server MariaDB-client galera-4
  
Configure Firewall and SELinux
  
Open TCP ports for Galera replication:
on-premise vms
[node1 ]# firewall-cmd --zone=public --add-port=4567/tcp --permanent
[node1 ]# firewall-cmd --zone=public --add-port=4568/tcp --permanent
[node1 ]# firewall-cmd --zone=public --add-port=4444/tcp --permanent

[node1 ]# firewall-cmd --reload
  
