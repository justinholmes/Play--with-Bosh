## BOSH Sample Release

This is a sample release repository for [BOSH](https://github.com/cloudfoundry/bosh) that deploys a three tier LAMP application: a wordpress blog which consists of a number of apache servers running php & wordpress, fronted by nginx, and using one mysql database for storage.

### Deploy

To deploy the sample application edit the example deployment manifest (located at the /examples directory) and adapt it with your data. Then use the following command sequence:

    bosh upload release releases/wordpress-2.yml
    bosh deployment <wordpress deployment manifest>
    bosh deploy

### Contents

There are three main directories in the release:

* src: this is the source code for the packages
* packages: these are the instructions on how to compile the source into binaries
* jobs: these are the scripts and configuration files required to run the packages

#### Packages

A package is made up of the following files:

* spec: defines the package name, the source file it uses and optionally other packages it depends on to compile
* pre_packaging: an optional file that prepares the source for the packaging script
* packing: the script that compiles the source into binaries

The sample is made up of 8 packages:

* apache2
* common
* debian_nfs_server
* mysql
* mysqlclient
* nginx
* php5
* wordpress

#### Jobs

A job is made up of the following files:

* spec: defines the job name, package dependencies, how to convert templates into files, and the properties used at templates
* monit: the monit file which defines how to start and stop the job
* templates: a directory which contain the scripts and config files for the job

The sample is made up of four jobs:

* nfs server, which consist of common + debian_nfs_server packages
* mysql, which consist of mysqlclient + mysql packages
* nginx, which consist of nginx package
* wordpress, which consist of mysqlclient + apache2 + php5 + wordpress packages

#### TODO

Use [HyperDB](http://wordpress.org/extend/plugins/hyperdb/installation/) & [MySQL master/slave replication](http://dev.mysql.com/doc/refman/5.1/en/replication-howto.html)



