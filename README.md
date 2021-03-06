## Setting up RabbitMq cluster locally using Docker and Docker-compose

- Create haproxy docker image for the cluster

    `docker build -t haproxy-rabbitmq-cluster:1.7 .`
- run the cluster

    `docker-compose up`

- Starts three rabbitmq and one haproxy load balancer
- In a new terminal, run these commands to connect rabbi2 and rabbit3 to the cluster
    
    `docker exec -it rabbit2 rabbitmqctl stop_app`

    `docker exec -it rabbit3 rabbitmqctl stop_app`

    `docker exec -it rabbit2 rabbitmqctl join_cluster rabbit@rabbit1`
    
    `docker exec -it rabbit3 rabbitmqctl join_cluster rabbit@rabbit1`
    
    `docker exec -it rabbit2 rabbitmqctl start_app`
    
    `docker exec -it rabbit3 rabbitmqctl start_app`
- By now all the nodes joined the cluster

- Check the status of the cluster

    `docker exec -ti rabbit1 rabbitmqctl cluster_status`

- The admin user name and password is **guest/guest**

- Reference to rabbitmqctl commands 
https://rabbitmq.docs.pivotal.io/37/rabbit-web-docs/man/rabbitmqctl.1.man.html