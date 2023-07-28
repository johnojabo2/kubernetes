# MongoDB and Mongo Express Deployment on Kubernetes

This repository contains the necessary Kubernetes manifests to deploy MongoDB and Mongo Express applications on a Kubernetes cluster. MongoDB is a popular NoSQL database, and Mongo Express is a web-based administrative interface for MongoDB.

## Prerequisites

Before deploying MongoDB and Mongo Express, ensure you have the following prerequisites:

1. Kubernetes Cluster: You need access to a running Kubernetes cluster.
2. `kubectl`: Install the `kubectl` command-line tool and configure it to communicate with your Kubernetes cluster.
3. Docker: You should have Docker installed to build and push custom Docker images if needed.

## Deployment Steps

Follow the steps below to deploy MongoDB and Mongo Express on your Kubernetes cluster:

1. Clone the Repository:

   ```bash
   git clone https://github.com/johnojabo2/kubernetes.git
   cd kubernetes
   ```

2. Deploy the MongoDB ConfigMap:

   The ConfigMap `mongodb-configmap.yml` contains the database URL used by Mongo Express. You can customize this URL according to your MongoDB deployment.

   ```bash
   kubectl apply -f mongodb-configmap.yml
   ```

3. Deploy the MongoDB Secret:

   The Secret `mongo-secret.yml` contains sensitive data like the MongoDB root username and password, base64 encoded. Modify the values or create your own secret if needed.

   ```bash
   kubectl apply -f mongo-secrets.yml
   ```

4. Deploy MongoDB Deployment and Service:

   The `mongodb.yml` file defines the MongoDB Deployment and Service to expose the MongoDB instance within the cluster.

   ```bash
   kubectl apply -f mongo-deployment.yml
   ```

5. Deploy Mongo Express Deployment and Service:

   The `mongo-exp.yml` file defines the Mongo Express Deployment and Service to expose the Mongo Express web interface.

   ```bash
   kubectl apply -f mongo-exp.yml
   ```

6. Access Mongo Express:

   The Mongo Express web interface can be accessed via the NodePort or LoadBalancer service, depending on your Kubernetes environment.

   - For NodePort:
     - Obtain the NodePort by running: `kubectl get svc mongo-express-service`
     - Access Mongo Express using: `http://<node-ip>:<node-port>`

   - For LoadBalancer (if used):
     - Obtain the external IP by running: `kubectl get svc mongo-express-service`
     - Access Mongo Express using: `http://<external-ip>:8081`

## Cleanup

To remove the MongoDB and Mongo Express deployments from your Kubernetes cluster, run the following commands:

```bash
kubectl delete deployment mongodb-deployment mongo-express-deployment
kubectl delete service mongodb-service mongo-express-service
kubectl delete secret mongo-secret
kubectl delete configmap mongodb-configmap
```

## Customization

Feel free to modify the YAML files according to your specific requirements. You can adjust the number of replicas, container images, ports, environment variables, or other settings to suit your application needs.

## Disclaimer

This deployment is intended for development or testing purposes. For production use, consider security best practices, such as enabling authentication and using secure connections.

**Happy Kubernetes Deployment!**
