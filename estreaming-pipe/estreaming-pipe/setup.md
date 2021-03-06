# Necessary client side setup

In order to work with _eStreaming Pipe_ you need to do the following: 

1. Develop HTTP server which will receive incoming messages as compressed CSV files in body of POST requests. Don't forget to list desired port \(typically 80\) in your instances security group inbound rules.
2. Create [Amazon Web Services](https://aws.amazon.com/) account \(if you do not have one\) 
3. Deploy this application in eu-west-1 \(EU Ireland\) AWS region. 
4. Setup VPC Endpoint Services to the application from previous step. In order to do it you should follow the steps from [corresponding AWS Manual](https://docs.aws.amazon.com/vpc/latest/userguide/endpoint-service.html) and complete steps required for "service provider". The following are the general steps to create an endpoint service:
   * Create a Network Load Balancer for your application in your VPC. The load balancer receives HTTP POST requests from us and routes it to your service. For more information, see [Getting Started with Network Load Balancers](https://docs.aws.amazon.com/elasticloadbalancing/latest/network/network-load-balancer-getting-started.html) in the AWS User Guide for Network Load Balancers. 
   * Create a VPC endpoint service configuration and specify your Network Load Balancer. 
   * After you've created your endpoint service configuration, authorize our account to create an interface endpoint to connect to your service. To do it you should add  permissions for a principal **arn:aws:iam::408064982279:root**
   * Inform us about your VPC Endpoint.

_Your AWS account will be charged for data transfer and VPC endpoint-hour consumed according to current_ [_AWS PrivateLink pricing_](https://aws.amazon.com/privatelink/pricing/) _in region you use. Plus you will pay for_ [_AWS Network Load balancer_](https://aws.amazon.com/elasticloadbalancing/pricing/?nc=sn&loc=3) _service depending on it's usage. Price of hosting your application and data storage is dependant on configuration of your choice and used AWS products._

