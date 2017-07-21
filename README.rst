GCloud Deployment Manager Template for AlertLogic Threat Manager
================================================================
Use this template to deploy Alert Logic Threat Manager into your existing GCloud infrasturcture.

Requirements
------------
* copy the al-threat-appliance from Alert Logic storage
* Gcloud project with network and subnet created
* Alert Logic account and unique registration key

Sample usage
------------
1. Copy this template to your working directory, i.e. al_tm_deploy.jinja

2. Run this command to copy Alert Logic Threat Manager image to your Gcloud storage ::

    gcloud compute images create al-threat-appliance --source-uri=https://storage.googleapis.com/threat/al-threat-appliance.tar.gz

3. Replace the parameters to match your environment and run this command ::

    gcloud deployment-manager deployments create deployment-name --config ./al_tm_deploy.jinja --properties region:us-central1,zone:us-central1-a,network:al-net,sub_network:al-net-1,firewall_tag:al-tmc,claim_cidr:0.0.0.0/0,network_cidr:10.5.0.0/16,machine_image:al-threat-appliance,machine_type:n1-standard-4

4. open HTTP://external-ip

5. enter unique registration code to claim the appliance

Required parameters
-------------------
  * region : target region to deploy this appliance, i.e. us-central1
  * zone : zone for the TM appliance, i.e. us-central1-a
  * network : network name for the TM appliance
  * sub_network : subnet name inside the network 
  * firewall_tag : target tag to be assigned for firewall rules
  * claim_cidr : source IP CIDR that is allowed to perform web claim on port 80, i.e. 0.0.0.0/0 or specific subnet range
  * network_cidr : network CIDR for the TM appliance (not subnet / sub network CIDR)
  * machine_image : image name for Threat Appliance
  * machine_type : minimum recommendation is n1-standard-4

License and Authors
===================
License:
Distributed under the Apache 2.0 license.

Authors: 
Welly Siauw (welly.siauw@alertlogic.com)