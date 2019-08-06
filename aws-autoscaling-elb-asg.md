# Notes for course "AWS: autoscaling applications with ELB and ASG"

* Ping PHP: https://gist.github.com/fiunchinho/2ee6013ce85a05f2b60a08c415973a12
* Use of `dig`: https://rm-rf.es/como-usar-el-comando-dig-ejemplos/
* The load balancer can have two different schemes:
  - public: **internet-facing**, it gets a public IP.
  - **internal**: it will only receive requests from the same VPC. The DNS assigned to the balancer resolves to a private IP.

* Configure a Security Group for the balancer: allowing HTTP inbound traffic from anywhere.
* Then, the EC2 instance with the app, should have a SG with an inbound rule to allow traffic from the SG assigned to the balancer.
* We can create three different type of balancers:
  - **Application Load Balancer**: for HTTP(S). We can use HTTP concepts (URL path, host), in order to define how you want the LB to balance the load.
    - If you choose HTTPS, you need to configure a certificate: you can have them for free from *Let's encrypt* and also from Amazon (ACM: AWS Certificate Manager).
  - **Network Load Balancer**: for TCP traffic, e.g. for sending logs to several Logstash instances.
  - Classic Load Balancer: old balancer, not recommended. For HTTP(S) and TCP. Only to be used if we have very old EC2 instances, when VPC didn't even exist.
* Configure:
  - a Security Group for the Load Balancer.
  - **Target Groups**: you define the group of EC2 instances than can receive the traffic from the LB.
  - **Listeners**: the ports where the LB will be listening to receive requests.
  - **Health check**: the path of the target group where, periodically, the LB will make a request to see if the EC2 instances are still alive.
    - **Advanced health check settings**: threshold, timeout, interval, HTTP success status code 
  - **Register targets**: you select the EC2 instances that you want to be a part of the target group.
* A LB does not send traffic to a new instance until having checked that it is healthy (it answers).   
  
  
  ## Doubts
  * What is the algorithm for balancing? Pure round-robin?
  * Is it possible to configure an algorithm base on CPU-Memory consumption?
