# Overview
This playbook can be used to remotely update the Seqware workflow. The playbook uses a copy of the new workflow that needs to be downloaded locally first instead of getting the new workflow (>12 GB) from S3 each time, as this saves time, bandwidth and money.

## Using the playbook

The following should be run from the Bindle server (replace workflow name and URI accordingly):


	git https://github.com/ICGC-TCGA-PanCancer/pancancer-bag.git
	cd pancancer-bag
	wget -O workflow-update/roles/update_workflow/files/Workflow_Bundle_SangerPancancerCgpCnIndelSnvStr_1.0.4_SeqWare_1.1.0-alpha.5.zip https://s3.amazonaws.com/oicr.workflow.bundles/released-bundles/Workflow_Bundle_SangerPancancerCgpCnIndelSnvStr_1.0.4_SeqWare_1.1.0-alpha.5.zip 
	cd workflow-update 

Edit the “inventory” file and add the addresses of the VMs.
Edit "workflow-update/roles/update_workflow/vars/main.yml" and specify the name of the new workflow, making sure you exclude the ".zip" extension.

Run the following command from the workflow-update directory:
	ansible-playbook -i inventory site.yml

