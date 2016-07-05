Table of Contents
=================

-  `CI Structure <#ci-structure>`__
-  `Script Documentation <#script-documentation>`__

   -  'install-and-check.sh <#install-and-check.sh>'__

CI Structure
============
For an example Jenkins configuration see.
::

   |https://ci.centos.org/view/rdo/view/POC/job/poc-browbeat-tripleo-quickstart-mitaka-delorean-full-deploy-minimal/

If you would like to make your own CI job that includes Browbeat please add your CI script to this directory and invoke it as minimally as possible on the Jenkins end, this will help us keep script changes in the repository and better test them before merging. 

Script Documentation
====================

install-and-check.sh
--------------------

