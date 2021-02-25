# distributed-tracing-workshop

These instructions are for Zipkin & the Online Boutique sample app. For Jaeger & HotROD instructions, visit [Jaeger Instructions](./jaeger.md)

## Hands-on Exercise 1 - Install Zipkin & Online Boutique sample app

To start Zipkin on your computer or laptop, you need to start Docker Desktop and follow instructions here:

```
https://github.com/hypertrace/hypertrace-samples/tree/zipkn_demo
```

Now, you can visit the Zipkin dashboard at http://localhost:9411. Once you have Zipkin running, you can send traces to Zipkin with the Online Boutique sample app. To run it, open a new terminal window and run the following:

```
$ kubectl create namespace online-boutique
$ kubectl apply -f online-boutique-demo/release/kubernetes-manifests.yaml --namespace online-boutique
$ kubectl get pods -n online-boutique
```

Visit the Online Boutique app at http://localhost:8080. Click on some items and purchase them. Each order generates traces. 

View your trace data in Zipkin at http://localhost:9411. 

To stop the Zipkin & Online Boutique containers

```
Docker container list
docker stop [container id]
```

## Hands-on Exercise 2 - Install Hypertrace & Online Boutique sample app

- Install Hypertrace on K8s using EKS: https://blog.hypertrace.org/blog/hypertrace-on-aws-eks/ 
- Install Hypertrace on K8s using Docker Desktop & Helm: https://docs.hypertrace.org/deployments/docker/

Now, let’s run Boutique again with Hypertrace-oc-collector endpoint, using command below:

```
$ kubectl create namespace online-boutique
$ kubectl apply -f online-boutique-demo/release/kubernetes-manifests.yaml --namespace online-boutique
$ kubectl get pods -n online-boutique

```

Now, visit the Boutique app at http://kubernetes.docker.internal. Click on some items and purchase them. Each order generates traces.  

View your trace data at http://localhost:2020


