# Finding Evil with Mitre Att&ck and the Elastic Stack

### High level flow

* Setup a new elastic cloud cluster
* Spin up a Strigo based Linux Environment
* Download Auditbeat
* Configure Auditbeat with Att&ck auditd ttp rules to output to Elastic cloud
* Have users go through some local ttp’s via command line
* Run through how it’s captured in Elastic
* Close with overview of ECS

Log into your Elastic Cloud Kibana instance.

Select the ‘Add Security Data’.

Select Auditbeat

Under ‘Getting Started’, select ‘DEB’

Follow the install instructions to download and install with the dbkg.

__Do not manually edit the auditbeat.yml as instructed in Kabana.__  

#### Set the cloudid and cloud authentication in the auditbeat keystore.

`echo "YOUR_CLOUD_ID"|sudo auditbeat keystore add CLOUD_ID --stdin`                                                                                                                                                                      

`echo "elastic:YOUR_PASSWORD"|sudo auditbeat keystore add --stdin CLOUD_AUTH`

#### Change to root  

`sudo -s`

##### Add configuration. Run these only once, please.

`echo 'cloud.id: "${CLOUD_ID}"'>> /etc/auditbeat/auditbeat.yml`

`echo 'cloud.auth: "${CLOUD_AUTH}"'>> /etc/auditbeat/auditbeat.yml`

##### Download the Att&ck based

`cd /etc/auditbeat/audit.rules.d`

`wget https://bit.ly/2Y9nhXb`

`mv 2Y9nhXb attack.rules.conf`

##### Login out
 `exit`                                                                              
##### Start Auditbeat

`sudo service auditbeat start`
