# Deploying OpenShift 4.3 on Baremetal Server

![Architecture](https://github.com/ekambaraml/ocp43-on-baremetal/blob/master/ocp43-deployment.png)

### Key Components

component | Description |
----------|-------------|
KVM | Kernel Based Virtual Machine, the virtualization layer technology used to provide the VMs on the bare metal host.|
DNSMasq | Combines a DNS forwarder, DHCP server and network boot features that enable new VMs to obtain IP addresses, and load operating systems from a PXE server, and provide DNS services to external and internal addresses.|
iPXE | Implementation of the Preboot eXecution Environment that allows operating systems to be installed via the network.|
Matchbox | A service that matches machine profiles to network boot configurations. This is how a new VM request knows which OS to request the ignition and other setup resources.|
GoBetween | A load balancer |



### Steps:


### 1. Setup RedHat Openshift subscription
![RH](https://github.com/ekambaraml/ocp43-on-baremetal/blob/master/rh1.png)

### 2. Provision Baremetal Server

![baremetal](https://github.com/ekambaraml/ocp43-on-baremetal/blob/master/baremetal.png)

Once the baremetal server is ready, log into the server and clone this githup repository
```
   $ ssh root@<baremetal server>
   $ git clone https://github.com/ekambaraml/ocp43-on-baremetal.git
   
```

### 3. Get pull Secrets

Login into RedHat URL https://cloud.redhat.com/openshift/install for downloading pull secrets and installer.

![RH](https://github.com/ekambaraml/ocp43-on-baremetal/blob/master/rh2.png)

copy pull-secret.json under the ocp43-on-baremetal folder

```
$ cp pull-secret.json ~/ocp43-on-baremetal
```

### 4. Prepare baremetal server

```
$ cd ~/ocp43-on-baremetal/scripts
$ sh prepare_host.sh
```

### 5. Setup Network

```
$ sh setup-network.sh
```

### 6. Setup Matchbox

```
$ sh setup-matchbox.sh 4.3.8
```

### 7. Setup Installer

```
$ sh setup-installer.sh 4.3.8
```

### 8. Setup Loadbalancer

```
$ sh setup-loadbalancer.sh 
```

### 9. Setup Bootstrap
```
$ sh bootstrap.sh
```

### 10. Setup NFS server
```
$ sh setup-nfs.sh 

```
### 11. Add User

```
$ sh setup-users.sh
```

### 12. Configure Internal Registry

