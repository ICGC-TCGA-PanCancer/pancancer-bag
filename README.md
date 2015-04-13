pancancer-bag
=============

This contains Bash scripts that deploy a [SeqWare](https://github.com/SeqWare) cluster with pan-cancer customizations for [Bindle](https://github.com/CloudBindle/Bindle)

Currently, this playbook has a dependency on [seqware-bag](https://github.com/SeqWare/seqware-bag) which needs to be checked out in a directory with the same parent directory. 

The sample\_configs directory contains a number of config files in order to install a pan-cancer cluster either as a cluster or as a single note, with BWA installed or without. 


## Detailed Description of Templates

The TCGA/ICGC PanCancer project is using Bindle to create analytical
nodes/clusters for use with a BWA Workflow and downstream variant calling
workflows. This project is using a variety of cloud technologies including
VirtualBox, OpenStack, and vCloud.  For each environment we use Bindle
to create SeqWare environments that utilize Oozie-SGE.  This allows researchers
to write workflows using SeqWare but also analytical pipelines that simply use
SGE and "qsub" to process data.

Here are some examples, you will want to customize the
~/.bindle/platform.cfg

to include the settings for the particular cloud
environment you are working in (EBI, BioNimbus, DKFZ, Korea, etc).  Each cloud
will provide you the specifics such as account name, API keys, and which cloud
technology to use.

    # launch, use the correct command line args for you 
    perl bin/launch_cluster.pl --config=openstack --custom-params=<cluster-name>


For provisioning in the Bindle configuration file specify:

    workflows = (comma separated list of workflows to be installed)
    
As an example to install BWA and HelloWorld, you require the following:

    install_workflow = True
    workflow_name = BWA
    workflows=Workflow_Bundle_BWA_2.6.3_SeqWare_1.1.0-alpha.5,Workflow_Bundle_HelloWorld_1.0-SNAPSHOT_SeqWare_1.1.0-alpha.5


Please see the [PanCancer Wiki](https://wiki.oicr.on.ca/display/PANCANCER) for
more information about this project.


!!! Important !!!
If running this on EBI or other cloud where large memory instances are not available, enable the "SGE hack" by passing sge_hack and swap_on as variables on the command line or throught the Bindle configuration file.

## For DKFZ/EMBL
If you are going to run the DKFZ/EMBL workflow, you will need to run the DEWrapperWorkflow playbook. To do this, ensure that you specify `DEWrapper` in your config file:


    install_workflow = True
    workflow_name = DEWrapper
    workflows=Workflow_Bundle_DEWrapperWorkflow_1.0-SNAPSHOT_SeqWare_1.1.0-rc.1

On your launcher, you must also have valid AWS configuration files as:

    ~/.aws/config
    ~/.aws/credentials

These files are need by part of the DEWrapper playbook. If you don't have a valid AWS login, the playbook will fail.
