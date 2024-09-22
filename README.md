# K8S-Deployment-Strategies

In Kubernetes we have multiple strategies among them we are discussing few of them here.
---------------------------------------------------
1) Rolling upate:
   -----
   a) It is the default strategy in kubernetes.
   
   b) It incrementally replaces replicaset of old version pods to the new replica set of new pods of new version.
   
   c) By default kubernetes will have maxunavailable and maxsurge is 25% where the rolling updates happens incrementally.
   
   d) It reduces almost downtime while updating new versions of applications.

   e) Suppose if you have created a service and rolling update is not taken place properly (i.e., only 25% of your whole deployment) the service
   will deviate the traffic only to the working pods.

2) Canary Deployment:
   -----
   a) It is most followed approach where you can test with real time application in production environment.

   b) New version of application is tested only with few set of users, where you will define in the annonations part that only 90% has to goto version v1
   and 10% has to goto version v2(few set of users)

   c) We require Ingress in order to test this kind of deployment. As a example we can take nginx canary deployment.

     ** https://kubernetes.github.io/ingress-nginx/examples/canary/**

   d) We can immediate revert back the changes(in annonations part) to the old version if the set of users tested new application is not upto the mark.

   As a summary in the above nginx canary deployment:
   ------
   1) You will creating main and canary deployments and services to the both main and canary

   2) You will also create ingress to both main and canary but while creatin ingress with canary you will writing annonations part like below
      annotations:
          nginx.ingress.kubernetes.io/canary: \"true\"
          nginx.ingress.kubernetes.io/canary-weight: \"50\"
      
   4) Ingress controller will watch both main and canary ingress resources and created LB and tell LB please send the traffic 50% to canary and 50% to main.

   5) Also please go through the above canary example as well.

          
   

   
