

# K8sRedisExercise

## Requirements:
- A laptop / virtual machines with 8GB RAM
- Gitlab account
- Docker
- Kubectl
- Redis 6.x

## The main goal:
### Deploy  redis on top of k8s cluster with security enabled and set redis logging to debug mode

 - ####  we  use StatefulSet to deploy the redis
    #### reason:
   
     A Redis pod that has access to a volume, but we want it to maintain access to the same volume even if it is redeployed or restarted
     we need a stable network identity and persistent volumes 
  
 
