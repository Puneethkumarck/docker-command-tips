
Docker-Clustering using Docker-swarm
====================================

- Background of docker swarm
  - Introduced from docker version 1.12
  - Natively managing a cluster of Docker engines called a swarm.
  - docker CLI to create a swarm, deploy apps, and manage a swarm 
    Optional feature; needs to be explicitly enabled
  - it will save us from single point of failure
  
  
 - Swarm Mode
   - Declarative state model.
   - _Self-organizing_ and *self-healing*.
   - Service discovery,load balancing ,and scaling.
   - rolling updates.
   
 - Swarm Mode:Protocols
   - Swarm Manager (Raft Consensus Group) manages  >>>>>>>>>> Swarm Worker nothing but containers
     
 - secure By default
   - Manager node composed with (TLS & CA) <-> Manager node (TLS &CA) <-> Manager node (TLS & CA)
   - worker composed with TLS <-> worker (TLS) <-> worker (TLS)
   
 - docker swarm commands (docker swarm --help)
   
      | commands | descrption
      | ---------|:-----------
      | ca       | display and rotate root ca
      | init     | Initilize a swarm
      | join     | Join a swarm 
      | join-token| manage join tokens
      | leave    | leave the swarm
      | unlock   | unlock the swarm
      | unlock-key | manage the unlock key
      | update   | update the swarm
      
 - initlilize swarm in MACOS 
 
 ```
 bash-3.2$ docker swarm init
 
    Swarm initialized: current node (w79ni1g3qdt6ik4v0c7po3p4w) is now a manager.

    To add a worker to this swarm, run the following command:

    docker swarm join --token SWMTKN-1-3yrhv4dhmnwym0pz2wc2dscjyw51yb58qlz8a7hr7yprt4ddc7-90pxcbhcmjtq6o4d6tafcvx1s 192.168.65.3:2377

    To add a manager to this swarm, run 'docker swarm join-token manager' and follow the instructions.
 ```
 
 - docker swarm leave
 
 ```
  bash-3.2$ docker swarm leave
  Error response from daemon: You are attempting to leave the swarm on a node that is participating as a manager. Removing the last manager erases all current state of the swarm. Use `--force` to ignore this message.
 ```
 
 - docker init in windows system
 
 ```
 docker swarm init --advertise--addr 192.168.99.100
 ```
 
 
Multinode Swarm Node Cluster
============================

- docker swarm mode initiliz --> docker swarm init --listen-addr <ip>  (other manager / worker node will join --listenaddr)
- worker machine joining manager --> docker swarm join --token <worker_token> <manager> 
- secondary manager join cluster--> docker swarm join --manger --token <manager_token> --listen-addr <master2> <master1>
  
    
