

# K8sRedisExercise

## Requirements:
- A laptop / virtual machines with 8GB RAM
- Gitlab account
- Docker
- Kubectl
- Redis 6.x

## The main goal:
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
      -  git clone  https://github.com/gansky770/K8sRedisExercise.git
      -  kubectl apply -f . (*command should be run from the YAML files directory*)

     - curl -L https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash) 
