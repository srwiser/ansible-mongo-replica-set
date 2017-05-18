Deployment of a mongodb replicaset with authN / authZ
-----------------------------------------------------

This playbook setup a MongoDB replicaset with
* user authentication / authorization
* secure communication between the nodes (using key file).

Inventory
---------

The inventory/ENVIRONMENT.ini file defines the hosts (primary and secondaries) used for the replicaset.  
On top the host decalration, some databasqe parameters are defined

```
[primary]
PRIMARY_IP

[secondary]
SECONDARY_1_IP
SECONDARY_2_IP

[primary:vars]
db_user_admin_username=USER_ADMIN_USERNAME
db_user_admin_password=USER_ADMIN_PASSWORD
db_cluster_admin_username=CLUSTER_ADMIN_USERNAME
db_cluster_admin_password=CLUSTER_ADMIN_PASSWORD
db_user_name=DB_USERNAME
db_user_password=DB_PASSWORD
db_name=DB_NAME
```

Nodes initialisation
--------------------


```ansible-playbook -i inventory/ENVIRONMENT.ini -k -u ssh_user_name -s init.yml```

```ansible-playbook -i inventory/ENVIRONMENT.ini main.yml --extra-vars '{"replSet":"replicasetname"}'```

If you want to cleanup everything

```ansible-playbook -i inventory/ENVIRONMENT.ini clean.yml```


