#Check VMWare API

I have taken this script from https://kb.op5.com/display/PLUGINS/Check+VMware+API+nagios+plugin and modified it to work with Monitoring::Plugin.

It was originally designed to work with Nagios::Plugin, but it is no longer available.

## Monitoring ESXi Machines with Nagios

I was looking for a way to monitor my ESXi 6.0 machine and stumbled upon a script. However there were few issues with the script and I had to modify it.

##Dependency Packages

I'd assume you have a working Perl installation. Please install following packages using yum as well.

```bash
yum intall cpanm
yum erase perl-XML-SAX-Base-1.04-1.el6.rf.noarch
yum install perl-XML-SAX
yum install perl-Nagios-Plugin libuuid* perl-XML-LibXML
yum install perl-Crypt-SSLeay
yum install openssl-devel
yum install libuuid-devel perl-YAML perl-Devel-CheckLib gcc perl-CPAN libxml2-devel.x86_64
```

Also install the following Perl modules using CPAN and CPANM

```bash
cpan -i JSON::PP
cpan -i Fatal
cpan -i Class::MethodMaker
cpan -i Env
cpan -i Class::MethodMaker

cpanm Params::Validate
cpanm Monitoring::Plugin
cpanm XML::LibXML::Common XML::LibXML Class::MethodMaker
``` 

##Installing vSphere Perl SDK for vSphere 6.0

Download vSphere Perl SDK for vSphere 6.0 from VMware downloads

Run the installation script in downloaded SDK to install as below,

```bash
./vmware-install.pl --prefix=/opt/vmwarecli EULA_AGREED=yes
 ```
 
##Running the Script

Now you should be able to run the script and get status from the ESXi server.

EG:

To get CPU usage,

```bash
./check_vmware_api.pl -D hypervisor1 -u ESXi_USER -p ESXi_PASSWORD -l cpu -s useage -w 92 -c 98
```

To get up time,

```bash
./check_vmware_api.pl -H hypervisor1 -u ESXi_USER -p ESXi_PASSWORD -l uptime
```

Please run the script as below to get a full list of available options

```bash
./check_vmware_api.pl
```
