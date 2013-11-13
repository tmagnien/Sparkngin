Sparkngin
==========
Pronounced Spark Engine  

Sparkngin is a high-performance persistent message logger built on Nginx

Out of the box includes:
- persistent kafka client Realtime streaming logs to Kafka
- heart beat
- log cleanup
- Connection retries when it looses connection to log destination
- Log persistence if the log consumer connection is down

Additonal:
- Monitoring with Ganglia
- Heart Alerting with Nagios


This is part of [NeverwinterDP](https://github.com/DemandCube/NeverwinterDP)

Community
====
- [Mailing List](https://groups.google.com/forum/#!forum/sparkngin)
- IRC channel #Sparkngin on irc.freenode.net


The Problem
======
The core problem is how to log data from a rest call and log it in high-performance way that 
allows for the delivery of messages to Kafka even when the connection is down.

Potential Implementation Strategies
======
There is a question of how to implement quaranteed delivery of logs to kafka.  
- Implement Avro Protocol?
- nginx write to ipc pipe -> secondary application that logs to disk and kafka
- nginx write to zmq -> secondary application that logs to disk and kafka
- nginx direct kafka driver that also spools to disk


Example Flow
=====
Application sending messages -> Sparkngin [ Nginx -> Zeromq (Publisher) -> Zeromq (Subscriber) -> Kafka (Client call "Producer") ] -> Kafka -> (Client called consumer) -> Some Application

Roadmap
======
- M0.1
- [Issue: 1 - Document proposed high level Architecture for Sparkngin](https://github.com/DemandCube/Sparkngin/issues/1)
- [Issue: 2 - Create mockup of new configuration directives that Sparkngin will provide](https://github.com/DemandCube/Sparkngin/issues/2)
- [Issue: 3 - Create nginx configuration for Sparkngin](https://github.com/DemandCube/Sparkngin/issues/3)
- [Issue: 4 - Create sample zeromq socket reader python commandline application](https://github.com/DemandCube/Sparkngin/issues/4)
- [Issue: 5 - Create sample zeromq socket reader c commandline application](https://github.com/DemandCube/Sparkngin/issues/5)

Feature Todo
======
- [ ] Architecture Proposal
- [ ] Sparkngin -> Zeromq (raw)
- [ ] Sparkngin -> Zeromq (NW protocol V1 - see below) 
- [ ] Zeromq -> Kafka
- [ ] Zeromq -> Flume
- [ ] Zeromq -> Syslog
- [ ] Ganglia Integration
- [ ] Nagios Integration
- [ ] Sparkngin Client (raw)
- [ ] Sparkngin Client (NW protocol V1)
- [ ] Heartbeat Agent
- [ ] Unix Man page
- [ ] Guide
- [ ] Build System - cmake or autotools
- [ ] Untar and Deploy - Work out of the box
- [ ] CentOS Package
- [ ] CentOS Repo Setup and Deploy of CentOS Package
- [ ] RHEL Package
- [ ] RHEL Repo Setup and Deploy of CentOS Package
- [ ] Mac DMG
- [ ] ZeroConf system
- [ ] HA logger
- [ ] Log stash integration
- [ ] Elastic search integration
- [ ] Sparkngin/Ambari Deployment
- [ ] Sparkngin/Ambari Monitoring/Ganglia
- [ ] Sparkngin/Ambari Notification/Nagios
- [ ] Event Schema Registration - json, avro, thrift protobuffs


NW Protocol V1
=====
Purpose is to provide standard event data that is used to allow for systematic monitoring, analytics, retries and timebased partition notifications (Aka send a message when all data from hour 1 is sent)
- timestamp
- ip of referrer
- topic
- env
- version
- submitted timestamp

Model Project to Eval
====
- <https://github.com/FRiCKLE/ngx_zeromq>
- <https://github.com/tailhook/zerogw>
- <http://openresty.org/>

Community Threads
====
- <http://stackoverflow.com/questions/8765385/mongrel2-vs-nginxzeromq>
- <http://stackoverflow.com/questions/15287196/websockets-behind-nginx-triggered-by-zeromq>

Resources to Learn Development
====
- <http://www.evanmiller.org/nginx-modules-guide.html>
- <http://www.evanmiller.org/nginx-modules-guide-advanced.html>
- <http://agentzh.org/misc/slides/nginx-conf-scripting/#1>
- <http://agentzh.org/misc/slides/recent-dev-nginx-conf/#1>
- <http://antoine.bonavita.free.fr/nginx_mod_dev_en.html>
- Hello World <http://blog.zhuzhaoyuan.com/2009/08/creating-a-hello-world-nginx-module/>
- Hello World Extended <http://usamadar.com/2012/09/02/writing-a-custom-nginx-module/>
- Other Hello World <http://nutrun.com/weblog/2009/08/15/hello-world-nginx-module.html>
- <https://github.com/perusio/nginx-hello-world-module>
- Intro Slides on Dev <http://www.slideshare.net/trygvevea/extending-functionality-in-nginx-with-modules>


Contributors
=====
- [Steve Morin](https://github.com/smorin)
- [Juan Manuel Clavijo](https://github.com/PROM3TH3U5)
- [Cui Yingjie](https://github.com/nihuo)
- [Ben Speakmon](https://github.com/bspeakmon)
 
FAQ
=====

- Why Sparkngin?

Sparkngin is mean to solve the short coming of realtime event streaming using restful endpoint.  Utilizing the logging and other connections in nginx is hard to configure and has limitations.

- Why trust Sparkngin?

Sparkngin is built on top of two main projects [Nginx](http://wiki.nginx.org/Main) which is the [worlds second most popular web server](http://news.netcraft.com/archives/2012/01/03/january-2012-web-server-survey.html) and [Zeromq](http://zeromq.org/) a high performance networking library.  Both provide a very solid core to realtime event streaming.  If you have questions about [why nginx](http://wiki.nginx.org/WhyUseIt), click the link.  Some people who use it are Facebook, [PInterest, Airbnb, Netflix, Hulu and Wordpress among others](http://wiki.nginx.org/Main).  Here is a summary of some nginx [benefits and features](http://www.wikivs.com/wiki/Apache_vs_nginx).


