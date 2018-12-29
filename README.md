# ansible-filebeat-install
PlayBook for Installing Filebeat in Various clients like
   - Postgres
   - Kafka/Zookeeper
   - Cassandra

﻿**Install Instructions**

Clone this repository using,

   git clone 


﻿**Pre-requisities**
- Hostfile formats
  
  [env-stack]
  hostname1.localdomain
  hostname2.localdomain
  
  ex:
  [dev-cassandra]
  devcassandra01.localdomain
  devcassandra02.localdomain

- Variables required to pass through commmand line
  
  envn=dev|qa|stg|prod (should match with your hostgroup to above)
  
  stack: technology (should match to your second part of group above)

- SSL (if you want to use SSL)
  
  sslmode=yes
  
  place your root.crt and root.key in the playbook directory with names server.key and server.crt
  
  These files will be copied to /etc/ssl_certs to the target hosts

- Elasticsearch hosts details and Kibana details
  
  Open filebeat.yml and replace output.elasticsearch add your elastic hosts
  
  Open filebeat.yml and replace kibana details and add user/password for your kibana


﻿**Run Playbook**

Ex:

**Multiple logs**

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=cassandra envn=stg logpath=“/var/log/cassandra/cassandra.log,/var/log/cassandra/system.log” sslmode=yes”

**All logs in specified directory**

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=cassandra envn=stg logpath=“/var/log/cassandra/*.log” sslmode=yes”


**For all Prod/QA/STG/Dev cassandra**

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=cassandra envn=dev logpath=“/var/log/cassandra/cassandra.log,/var/log/cassandra/system.log” sslmode=yes”

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=cassandra envn=qa logpath=“/var/log/cassandra/cassandra.log,/var/log/cassandra/system.log” sslmode=yes”

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=cassandra envn=prod logpath=“/var/log/cassandra/cassandra.log,/var/log/cassandra/system.log” sslmode=yes”

**For all Redis Prod/QA/STG/Dev**

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=redis envn=dev logpath=“/var/log/redis/*.log” sslmode=yes”

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=redis envn=qa logpath=“/var/log/redis/*.log” sslmode=yes”

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=redis envn=stg logpath=“/var/log/redis/*.log” sslmode=yes”

**For all Kafka Prod/QA/STG/Dev**

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=kafka envn=dev logpath=“/var/log/kafka/server.log”,”/var/log/kafka/controller.log” sslmode=yes”

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=kafka envn=qa logpath=“/var/log/kafka/server.log”,”/var/log/kafka/controller.log” sslmode=yes”

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=kafka envn=stg logpath=“/var/log/kafka/server.log”,”/var/log/kafka/controller.log” sslmode=yes”

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=kafka envn=prod logpath=“/var/log/kafka/server.log”,”/var/log/kafka/controller.log” sslmode=yes”

**For all Zookeeper servers Prod/QA/STG/Dev**

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=zookeeper envn=prod logpath=“/var/log/kafka/server.log”,”/var/log/kafka/controller.log” sslmode=yes”

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=zookeeper envn=dev logpath=“/var/log/kafka/server.log”,”/var/log/kafka/controller.log” sslmode=yes”

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=zookeeper envn=qa logpath=“/var/log/kafka/server.log”,”/var/log/kafka/controller.log” sslmode=yes”

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=zookeeper envn=stg logpath=“/var/log/kafka/server.log”,”/var/log/kafka/controller.log” sslmode=yes”

**For all postgres hosts**

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=postgres envn=dev logpath=“/data/pg/pg_log/*.log” sslmode=yes”

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=postgres envn=qa logpath=“/data/pg/pg_log/*.log” sslmode=yes”

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=postgres envn=stg logpath=“/data/pg/pg_log/*.log” sslmode=yes”

ansible-playbook -i hosts ansible-filebeat-install.yml --extra-vars “stack=postgres envn=prod logpath=“/data/pg/pg_log/*.log” sslmode=yes”
