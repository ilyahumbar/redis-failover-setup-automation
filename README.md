# redis-failover-setup-automation
A script which helps with setting up and running simple redis/sentinel failover configuration. Currently the script supports basic sentinel setup where sentinel instances are running on the same machines with redis-server instances (<a href="http://redis.io/topics/sentinel#example-2-basic-setup-with-three-boxes" target="_blank">Redis sentinel documentation</a>). Redis is compiled from sources. Redis-server and redis-sentinel are orchestrated by supervisor. Supervisor is installed from ubuntu package manager. This script should be run on each machine which should become a part of failover configuration. Flag ```-m``` is used to specify if current machine should be configured as a master instance.

## Prerequisites
The script is tested to work on clean Ubuntu 14.04 install. If you already have redis installed via package manager, please remove it and make sure all redis instances are stopped on the current machine to prevent any conflicts. You can also use ```-r``` option to remove redis previously installed from sources (/usr/local/bin). Be aware that this option also removes any associated logs and configuration files.

## Arguments
**-i** [required]
   Specify ip address for master instance.

**-w** [required]
  Password to be set to access redis server. Currently, this option is required to run the script.

**-m**
   Flag indicating that the current machine should be configured as a master. If this flag is not specified the machine will be configured as a slave.

**-v**=3.2.5
    Redis version to install from sources. The default is 3.2.5

**-p**=6379
  Redis port to configure redis-server instance to listen to. You can run multiple redis instances on the same machine under different ports. Separate configuration files are created for different ports. Sentinel port is derived from redis port by prefixing it with 2. If redis port is 6390 then sentinel port is 26390

**-q**=2
   Sentinel quorum. The default is 2

**-r**
   Flag indicating whether the script removes any existing redis binaries and all associated configuration.
