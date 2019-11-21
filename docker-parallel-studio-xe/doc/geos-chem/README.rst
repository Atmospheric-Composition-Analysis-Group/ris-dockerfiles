================
Docker Geos Chem
================

.. contents::
   :depth: 2
   :local:

The Docker Parallel Studio XE is a docker image for Intel Parallel Studio XE.

How to Build?
-------------

Shown below are the steps to build an ifort docker image.

1) Download `Geos Chem`_
2) Clone bitbucket repository `docker-parallel-studio-xe`__

.. code::

    git clone ssh://git@bitbucket.ris.wustl.edu:7999/appeng/docker-parallel-studio-xe.git

3) Change directory to the cloned repository

.. code::

    cd docker-parallel-studio-xe


4) Build a docker image

.. code::

    mkdir build
    cp Dockerfile.geos-chem build/Dockerfile
    cd build
    cp -r /your/intel-parallel-studio-xe/licenses .
    docker build --tag geos-chem .

.. _docker-parallel-studio-xe: ssh://git@bitbucket.ris.wustl.edu:7999/appeng/docker-parallel-studio-xe.git

How to run?
-----------

The docker image can be run using the command shown below.

.. code::

    docker run -it --rm geos-chem /bin/bash

Note: Please replace the "/your/licenses" with your Intel Studio XE licenses.

How to send a job to the compute1 cluster?
------------------------------------

The compute1 is set up to accept jobs that run in docker containers.  You can submit jobs with a docker image.
The docker image must be pushed to the Docker registry.  It can be public or RIS registry.  For demonstration
purposes, the docker image is pushed to the Docker hub registry with docker hub account `sleongmgi`.  Shown below
are the commands to accomplish that.

.. code::

   # Tag the docker image with the right tag
   docker tag geos-chem sleongmgi/geos-chem

   # Push the docker image
   docker push sleongmgi/geos-chem


Note: You should use your docker hub account or a private registry that can be seen by the compute1 cluster.

bsub
~~~~

The ``bsub`` command is how users launch LSF jobs.

Shown below is an example command that submits an interactive job to compute1 cluster.

.. code::

    bsub -q general-interactive -a "docker(sleongmgi/geos-chem)" -Is /bin/bash

References
----------

* `Docker`_
* `bsub`_
* `Intel® Parallel Studio XE`_

.. _Docker: https://www.docker.com/
.. _busb: https://www.ibm.com/support/knowledgecenter/en/SSETD4_9.1.2/lsf_command_ref/bsub.1.html
.. _Intel® Parallel Studio XE: https://softwarestore.intel.com/SuiteSelection/ParallelStudio

