### [Source of this study material : Google Cloud Data Engineer by Ankit Mistry](https://www.udemy.com/course/google-cloud-gcp-professional-data-engineer-certification/)


## Cloud Memorystore

- Fully managed **inmemory** database

- 2 engines currently supported inside the Memorystore:

  - Redis

  - Memcached

- Only internal IP address


## How to use Memorystore


- When you go to Memorystore, you can either choose Redis or Memcached. We'll go with Redis instance here.


![memory-store-ui](/GCP_pictures/Study-logs/memorystore/memorystore-ui.PNG "Memorystore UI")


- Configure your Redis instance according to your needs and click create.


![redis-instance-creation](/GCP_pictures/Study-logs/memorystore/configure-redis-instance.PNG "Configure Redis instance")


- It's created but because it has only an internal IP, we can't directly connect to it. So we will create a virtual machine to use it.


![redis-instance-created](/GCP_pictures/Study-logs/memorystore/redis-instance-created.PNG "Redis instance created")


- When creating a vm, we will use **the same network** as the Redis instance. 


![vm-creation](/GCP_pictures/Study-logs/memorystore/vm-creation.PNG "VM creation")


- Then, SSH into the vm and run some update command:


```
sudo apt update 
```

- After that, we need to install Redis inside the vm.


```
sudo apt install redis-tools
```

- Let's go back to the Redis instance and grab its internal IP address.


![redis-ip-address](/GCP_pictures/Study-logs/memorystore/redis-ip-address.PNG "Redis internal IP address")


- Now, let's connect our vm to the remote Redis host.


```
redis-cli -h 10.7.128.43
```


![redis-connected](/GCP_pictures/Study-logs/memorystore/redis-connected.PNG "Redis connected")


- When you ping, pong returned.


![ping-pong](/GCP_pictures/Study-logs/memorystore/ping-pong.PNG "Ping pong")


- When we use **set** command, it automatically suggests some command structure like key value. You can set key value pair here:


![set-command](/GCP_pictures/Study-logs/memorystore/set-command.PNG "Set command")


- When you set a specific key value pair, and when you use **get** command with a key, it simply returns the value.


![get-command](/GCP_pictures/Study-logs/memorystore/get-command.PNG "Get command")


- Let's quickly create another similar vm and see if the same key value pair exists there or not.


- Follow the same procedure like before to sudo update and install redis tools.


- And when you connect to the Redis CLI and check if the same key value pair exists, yes, it does!


![key-value-exists](/GCP_pictures/Study-logs/memorystore/key-value-saved.PNG "Key value retrieval")


