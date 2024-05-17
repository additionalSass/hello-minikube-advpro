# hello-minikube-advpro
1. Comparing Application Logs Before and After Exposing it as a Service:
Before exposure: Access was limited to direct interaction with the Pod. Logs would only reflect interactions originating from my local machine. 
I0517 11:36:31.392565       1 log.go:195] Started HTTP server on port 8080
I0517 11:36:31.392872       1 log.go:195] Started UDP server on port  8081
After exposure: The Service acts as an internal load balancer. Now I can open the app through some URL. Each time I open the app through the URL, the request is routed to a Pod within the deployment. This results in an increase in log entries as each interaction with the app, now routed through the Service, is recorded.
I0517 11:36:31.392565       1 log.go:195] Started HTTP server on port 8080
I0517 11:36:31.392872       1 log.go:195] Started UDP server on port  8081
I0517 11:41:49.441061       1 log.go:195] GET /
I0517 11:41:49.580342       1 log.go:195] GET /
2. Purpose of the -n option in kubectl get:
Well, the -n flag, is a shortened synonym of --namespace. It sets the namespace I want to interact with. Without the -n flag, kubectl will default to the "default" namespace.
So the reason the initial kubectl get invocations did not list some of the pods/services I created is because they were created in a not-"default" namespace, the kube-system namespace as suggested in the tutorial. Using kubectl get -n kube-system will make us able to view the resources within that specific namespace.