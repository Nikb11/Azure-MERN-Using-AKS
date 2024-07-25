
* Clone the git repository
```
https://github.com/UnpredictablePrashant/SampleMERNwithMicroservices
```
* Try to run in local and then create a docker file for each service.
* backend hello service 
```
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 4200
CMD [ "node","index.js" ]
```
* backend profile service 

```
FROM node:18
WORKDIR /app
COPY . .
RUN npm install
EXPOSE 4201
CMD [ "node","index.js" ]

```
* frontend
```
FROM node:18
WORKDIR /app
COPY package*.json /app
RUN npm install
COPY . /app
EXPOSE 3000
CMD [ "npm","start" ]

```
* create a repository in docker hub
```
docker build -t nikb11/micro_backend_helloservice:latest .
docker build -t nikb11/micro_backend_profileservice:latest .
docker build -t nikb11/micro_frontendservice:latest .

```
* pushed all the images to docker hub.
```
docker push nikb11/micro_backend_helloservice:latest 
docker push nikb11/micro_backend_profileservice:latest
docker push nikb11/micro_frontendservice:latest
```

* Creating AKS cluster 
```  
Go to Kubernetes service -> Create Kubernetes cluster -> create resource group -> cluster name & availability zones & kubernetes version & Authentication and Authorization -> Node pools (Adjust node size if needed ) -> Networking configure to Azure CNI & DNS name & network policy -> Integrations (create container registery) -> Monitoring Enable container logs -> Tags if needed -> Review and create 
```

* azure account login 
```
az login
```
* kubectl command to store credencials in kube config file

```
az aks get-credentials --resource-group aks-group --name micro-cluster1
```

* Deployent 

```
kubectl apply -f deploy.yaml
```
* validation
```
kubectl get pods
kubectl get svc 

```
* configured with DNS server.



