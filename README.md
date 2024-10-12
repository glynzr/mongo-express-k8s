I have created two deployments: one for MongoDB and the other for Mongo Express. To ensure that MongoDB is only accessible internally, I configured the mongo-express-service with a ClusterIP type, which is the default service type in Kubernetes. In contrast, since the Mongo Express deployment needs to be externally accessible, I used the LoadBalancer type for its service.

To follow best practices and avoid declaring database credentials directly in the deployment configuration, I created secrets using the following commands:
```bash
kubectl create secret generic db-user --from-literal=user=<username>
kubectl create secret generic db-password --from-literal=password=<password>
```
Additionally, Mongo Express needs to connect to MongoDB, so I will declare the MongoDB service URL in a ConfigMap and reference it in the mongo-express-deployment.
