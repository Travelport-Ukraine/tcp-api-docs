# Recommendations for use of AWS products for processing incoming data stream

From our quite a big experience we strongly _do not_ recommend to directly use any request-based priced services to process eStreaming data in your application. Like [API Gateway](https://aws.amazon.com/api-gateway/) for example. It is absolutely fantastic tool but for slightly different cases. The reason is if you will call API Gateway for each individual POST request you'll be charged $3.50 per million API calls received. However only GB market generates 300M-400M requests per month. Meanwhile there is a lot of many times cheaper scalable and powerful options. Here is the list of our recommendations how to build environment. 

The list is ordered from "Just perfect" to "Very good" to "Acceptable". The better configuration is the more experience and knowledge it requires to setup.

* [Elastic Beanstalk](https://aws.amazon.com/en/elasticbeanstalk/) to host HTTP server & receive incoming messages → [Kinesis](https://aws.amazon.com/kinesis/) to collect, buffer and deliver messages in butches → [Lambda](https://aws.amazon.com/lambda/) To run your processing code in serverless invorement
* [Elastic Beanstalk](https://aws.amazon.com/en/elasticbeanstalk/) to host HTTP server, receive incoming messages and pack them in a butches → [Lambda](https://aws.amazon.com/lambda/) To run your processing code in serverless invorement
* [Elastic Beanstalk](https://aws.amazon.com/en/elasticbeanstalk/) to host HTTP server, receive incoming messages and  run your processing code
* [EC2](https://aws.amazon.com/ec2/)  to host HTTP server, receive incoming messages, run your processing code and be responsible for all aspects of operation system and all other software running on your server

If you think that this setup could be complicated for you, the good news is we already did this for you in the most durable and cost effective way in our fully managed solution [eStreaming API](http://estrapi.cee-systems.com).
