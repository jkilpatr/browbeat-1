Table of Contents
=================

-  `CI Structure <#ci-structure>`__
-  `Script Documentation <#script-documentation>`__

   -  `Install and Check <#install-and-check>`__
   
      -  `Invoking Locally <#invoking-locally>`__

CI Structure
============
For an example Jenkins configuration see `this job <https://ci.centos.org/view/rdo/view/POC/job/poc-browbeat-tripleo-quickstart-mitaka-delorean-full-deploy-minimal/>`_

If you would like to make your own CI job add your CI script to this directory and invoke it as minimally as possible on the Jenkins end, this will help us keep script changes in the repository and better test them before merging. 

Script Documentation
====================

Install and Check
-----------------
Currently the main CI script that is run against every commit submittied to the Openstack Gerrit. For each test a fresh Openstack instance is deployed using `TripleO Quickstart <https:github.com/openstack/tripleo-quickstart>`_, Browbeat is then installed. Both of these happen regardless of what was included in the commit. Workload tests are run only if a file diff between the commit and Browbeat master contains the workload name. 

To add an additional workload to the script add the workload name to the tools loop near the bottom of the file. 

:: 

    for tool in rally perfkit shaker <tool name>; do

   
Then add configuration details that run all functions of the added task or plugin to the browbeat-compleate.yaml file in the repository top level. 

Invoking Locally
~~~~~~~~~~~~~~~~

To run install-and-check.sh using your local machine as the driver for a TripleO Quickstart / Browbeat deployment create an emptry directory to use as your workspace and point virthost at a machine running CentOS 7+ or RHEL 7+ with at least 32gb of ram. 

::

    $ export WORKSPACE=<your empty directory>  
    $ export VIRTHOST=<deployment machine hostname>

Navigate to the workspace direcotry

::

    $ cd $WORKSPACE

Clone the required repositories

::

    $ git clone https://github.com/openstack/browbeat
    $ git clone https://github.com/openstack/tripleo-quickstart/

Finally invoke the script and settle in, this command will take about two hours to compleate and will place all the relevent ssh credentials and other infromation to access your instance once the run is compleate in the workspace directory. 

::

    $ bash $WORKSPACE/browbeat/ci-scripts/install-and-check.sh mitaka delorean minimal periodic
