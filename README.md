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

Please see the [PanCancer Wiki](https://wiki.oicr.on.ca/display/PANCANCER) for
more information about this project.

!!! Important !!!
If running this on EBI or other cloud where large memory instances are not available, enable the "SGE hack" by passing sge_hack and swap_on as variables on the command line or throught the Bindle configuration file.
