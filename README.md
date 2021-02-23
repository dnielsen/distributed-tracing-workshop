# distributed-tracing-workshop

## Hands-on Exercise 1 - Install Jaeger & HotROD sample app

To start Jaeger on your computer or laptop, you need to start Docker Desktop and run this command :

```
docker run \
 --rm \
 --name jaeger \
 -p6831:6831/udp \
 -p16686:16686 \
 jaegertracing/all-in-one:latest
```

Now, you can visit the Jaeger dashboard at http://localhost:16686
Once you have Jaeger running, you can send traces to Jaeger with the HotROD sample app. To run HotROD, open a new terminal window and run the following:

```
docker run \
 --rm \
 --link jaeger \
 --env JAEGER_AGENT_HOST=jaeger \
 --env JAEGER_AGENT_PORT=6831 \
 -p8080-8083:8080-8083 \
 jaegertracing/example-hotrod:latest \
 all
```

Visit the HotROD app at http://localhost:8080. Click on a customers name to order a car. Each order generates traces. If you want to read more about HotROD read this blog post: https://medium.com/opentracing/take-opentracing-for-a-hotrod-ride-f6e3141f7941

To stop the Jaeger & HotROD containers

```
Docker container list
docker stop [container id]
```

## Hands-on Exercise 2 - Install Hypertrace & HotROD sample app

- Install Hypertrace on K8s using EKS: https://blog.hypertrace.org/blog/hypertrace-on-aws-eks/ 
- Install Hypertrace on K8s using Docker Desktop & Helm: https://docs.hypertrace.org/deployments/docker/

Now, let’s run HotRod again with Hypertrace-oc-collector endpoint, using command below:

```
docker run \
 --rm \
 --env JAEGER_ENDPOINT=http://<docker.for.mac.localhost or OC-collector endpoint from EKS>:14268/api/traces \
 -p8080-8083:8080-8083 \
 jaegertracing/example-hotrod:latest \
 all
```

Now, visit the HotROD app at http://localhost:8080. Click on a customer’s name to order a car. Each order generates traces. 

Visit hotrod app at http://localhost:8080 . View your trace data at http://localhost:2020


