# Elasticstack-ansible-vagrant

This repository offers a place to play around with Elastic stack 5.x.

Vagrant file describes two ubuntu 14.04 boxes.
* The one named ```elk``` is Elastic stack itself. Elasticsearch, Logstash, Kibana will be installed on that machine by default.
* The second box (```web```) will have a 3-tier application installed which includes NGINX, application written in GO, and a MySQL database. It will also have different beats (ligthweight shippers for LS and ES).

As you may notice, all the provisioning is done by using Ansible.

I tried to split all the main components into roles. So you're basically free to choose whatever you wish to install on your boxes. You simply need to edit two files for that - ```web.yml``` and ```elk.yml``` - which describe services that will be installed on the corresponding machines.

If you would like to install an existing service, let's say metricbeat on elk machine, simply edit/add a template for that machine in metricbeat's role folder (under templates). If you wish to try and install a new service, just add a new role and put it in the web.yml or elk.yml which are basically running lists for the boxes.

Using Ansible as a provisioner, also gives you the advantage of being able to deploy the services on any machine you want, not just the vagrant boxes described in  Vagrantfile.

I already did try different beats and logstash plugins by myself and put them in the repository. So you can collect and analyze all the basic logs and metrics. You'll also find here some sample logs and templates for elasticsearch and kibana. Hopefully, all that will give you an easy start on Elastic Stack.

P.S. All the testing has been done on ```ubuntu 14.04 64-bit```.

 #### How do I start?

 Vagrantfile is the first place you should look into, because it describes ip addresses of the machines as well as ports what will be available for your host machine.

 Fire up one machine (two machines):
 ```
 vagrant up elk (vagrant up)
 ```

 In you browser, type ```10.37.129.10:5061``` (if you haven't changed anything)  to start analyzing logs with Kibana.

 Metrics collection is defined only for the web machine by default. So if you started up 2 machines, default indices ans dashboards would be installed and you could see in action metrics and logs being collected. Just go to **Management -> Saved objects**, then choose **Metricbeat-overview**, for example, to see collected metrics.

 I would advise you take a look at the [getting started](https://www.elastic.co/guide/en/beats/libbeat/5.x/getting-started.html) with Elastic stack. They do a great job on explaining how things are configured.

 #### Sample data and examples
 I found some [sample logs and examples](https://github.com/elastic/examples) of how people configure and use Elastic stack. Feel free to use them and see what sort of things could be done with Elastic stack.

 Ssh to elk machine:
 ```
 vagrant ssh elk
 ```

 Then load sample logs to elasticsearch

 ```
 root@elk:/opt/elastic-stack-showcase/sample_data# cat apache_logs | /usr/share/logstash/bin/logstash --path.settings /etc/logstash/ -f example2/apache_logstash.conf
 ```
Go to **Kibana -> Management -> Index patters -> add new**.  Type ```apache_elk_example``` and create a new index pattern.


Load sample dashboard into Kibana from ```elastic-stack-showcase/sample_data/example2/apache_kibana.json``` : **Kibana -> Management -> Saved objects -> import**



Click on Dashboard tab and open Sample Dashboard for Apache Logs dashboard





 
