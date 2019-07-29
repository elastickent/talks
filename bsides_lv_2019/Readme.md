# Finding Evil with Mitre Att&ck and the Elastic Stack

### High level flow
* [Spin up a Strigo based Linux Environment](#strigo)
* [Setup a new elastic cloud cluster]()
* [Download Auditbeat](#download)
* [Configure Auditbeat with Att&ck auditd ttp rules to output to Elastic cloud](#configure)
* [Have users go through some local ttp’s via command line](#cmdline)
* [How it’s captured in Elastic](#capture)
* [Overview of ECS and SIEM](#siem)

<a name="strigo"/></a>
## Strigo
Go to [Strigo login](https://app.strigo.io/event/HrJm4zCyf9u7zKXda) 

<a name="cloud"/></a>
## Create your Elastic Cloud cluster.
[Go through the setup guide](https://docs.google.com/document/d/104kc_aZiyMzbmTfdxDyKMIQUG9sr5gkMR26j0pjFoFQ/edit?usp=sharing)
Log into your Elastic [Cloud Kibana](https://cloud.elastic.co/login) instance.


<a name="download"></a>
 ### Download Auditbeat
 
->Select the 'K' icon at the far left corner of Kibana.

->Select ‘Add Security Data’.

->Select Auditbeat

->Under ‘Getting Started’, select ‘DEB’

<a name="cmdline"/></a>
Follow the install instructions in Kibana to download and install with the dbkg only.

__Do not manually edit the auditbeat.yml as instructed in Kabana.__  

<a name="configure"/></a>
#### Att&ck Rules
[Auditd Attack Rules](https://gist.githubusercontent.com/elastickent/839e5f49f8846d67b254d9318095c101/raw/9a9d35454ecfcaf549b413ed104f1cee22121429/auditd-attack.rules.conf)
#### Set the cloudid and cloud authentication in the auditbeat keystore.

`echo "YOUR_CLOUD_ID"|sudo auditbeat keystore add CLOUD_ID --stdin`                                                                                                                                                                      
`echo "elastic:YOUR_PASSWORD"|sudo auditbeat keystore add --stdin CLOUD_AUTH`

#### Change to root  

`sudo -s`

##### Add configuration. Run these only once, please.

`echo 'cloud.id: "${CLOUD_ID}"'>> /etc/auditbeat/auditbeat.yml`

`echo 'cloud.auth: "${CLOUD_AUTH}"'>> /etc/auditbeat/auditbeat.yml`

##### Download the Att&ck based rules.

`cd /etc/auditbeat/audit.rules.d`

`wget https://bit.ly/2Y9nhXb`

`mv 2Y9nhXb attack.rules.conf`

##### Login out of the root account.
 `exit`                                                                              
##### Start Auditbeat

`sudo service auditbeat start`
<a name="cmdline"/></a>
#### 
