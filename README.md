

# K8sRedisExercise

## Requirements:
- A laptop / virtual machines with 8GB RAM
- Gitlab account
- Docker
- Kubectl
- Redis 6.x

## HANDS ON:
### Deploy  redis on top of k8s cluster with security enabled and set redis logging to debug mode

## Steps:
 - #### We use [StatefulSet](https://kubernetes.io/docs/concepts/workloads/controllers/statefulset/) to deploy the redis
    #### reason:
   
     A Redis pod that has access to a volume, but we want it to maintain access to the same volume even if it is redeployed or restarted
     we need a stable network identity and stable persistent volumes.
  - #### We use  [service](https://kubernetes.io/docs/concepts/services-networking/service/) to expose the redis pod  
    - StatefulSets require a [ headless service](https://kubernetes.io/docs/concepts/services-networking/service/#headless-services) to achieve 
      stable network identity .
     
  - #### We use [Configmap](https://kubernetes.io/docs/concepts/configuration/configmap/) to mount, configure and manage the redis configuration file - redis.conf   
     - To achieve  security enabled mode, we set the  "**protected-mode yes**" in redis.conf file.
     - To achieve debug mode ,we set the "**loglevel debug**" in redis.conf file

   - #### We will clone the repo with created YAML files in the cluster working node and deploy all the objects :
      -  $ git clone  https://github.com/gansky770/K8sRedisExercise.git
      -  $ kubectl apply -f . (*command should be run from the YAML files directory*)
    
  ## Bonus questions: 
  - ### **Steps needed to implement helm chart**
    - We deploy HELM on our k8s cluster by running the next command from the cluster node
      - $ curl -L https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash 
    - We run **"$ helm create k8sredis"**  command for creating the chart with name k8sredis
    - The helm Created k8sredis directory with generated template folder , for our exercise we will delete all files in this template folder and put there our YAML           files  from the git repo
    -   Finally  we run **"$ helm install k8sredis ./k8sredis"** command to deploy our chart (*k8sredis is the name of the release ./k8sredis the folder of the chart             repo we created*)
   - ### **Recommended Redis Helm chart** 
     - **softonic/redis-sharded --version 0.3.0**
     - ### How to deploy:
       - $ helm repo add softonic https://charts.softonic.io 
       - $ helm install my-redis-sharded softonic/redis-sharded --version 0.3.0
      - ### What features does it cover ? 
         This Helm Chart covers sharding feature,offers an easy way to use Redis with multiple independent master instances as shards, and optionally twemproxy in              front, so that the client can see it as a single redis instance.
         The main appeal of sharding a database is that it can help to facilitate horizontal scaling, Horizontal scaling is the practice of adding more instances              to an existing stack in order to spread out the load and allow for more traffic and faster processing. 
         Another benifit of a sharded database architecture is to speed up query response times. When you submit a query on a database that hasn’t been sharded,                it may have to search every row in the table you’re querying before it can find the result set you’re looking for. For an application with a large,                    monolithic database, queries can become prohibitively slow. By sharding one table into multiple, though, queries have to go over fewer rows and their                  result sets are returned much more quickly.
             
          #### How sharding works
                                           /- Redis (node 1)
              Client 1 ---                /-- Redis (node 2)
                           Redis Sharding --- Redis (node 3)
              Client 2 ---                \-- Redis (node 4)
                                           \- Redis (node 5)
             
             
             

