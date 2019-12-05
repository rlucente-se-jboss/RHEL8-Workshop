= RHEL8-Workshop

Foundational exercises to introduce core concepts of Red Hat Enterprise Linux 8

== Install a minimal VM

You can get the RHEL 8 ISO image for personal development use by registering for free at the https://developers.redhat.com[Red Hat Developer] portal.  Make sure to remember your username and password as you'll need that to register for package updates after you install RHEL.

* Download the https://developers.redhat.com/products/rhel/download[RHEL 8 DVD ISO image].  This is 7 GB in size so allow time for this to complete.
* Do a "minimal install" of RHEL 8 as a VM with default filesystems using your preferred virtualization environment.  I used Oracle's VirtualBox on my Mac OSX laptop and I assigned the VM the resources below.  Make sure to note the IP address assigned to the host-only adapter so you can ssh to the VM later.
** Eight GB memory
** 128 GB disk
** Four vCPUs
** Two network interfaces, NAT and Host-Only
* Open a terminal on your host (e.g. your laptop) and ssh to the RHEL 8 VM

    ssh root@VM_IP_ADDRESS
    subscription-manager register --username RH_DEVELOPER_USERNAME --auto-attach
    subscription-manager repos --disable='*'
    subscription-manager repos --enable=rhel-8-for-x86_64-baseos-rpms \
        --enable=rhel-8-for-x86_64-appstream-rpms \
        --enable=ansible-2-for-rhel-8-x86_64-rpms
    yum -y update
    yum -y install git ansible
    yum -y clean all
    reboot

== Prepare the Workshop

* Ensure you can ssh to root@localhost using an ssh key

    ssh-keygen 
    ssh-copy-id -i ~/.ssh/id_rsa.pub root@localhost
    ssh root@localhost

* Run the playbook to setup the lab

    cd ~/RHEL8-Workshop
    bash prepare-rhel8-workshop.sh 

Once the script is done, root and student users will be created with the password of "r3dh4t".

Master document for this branch can be found here:

[The Definitive Red Hat Enterprise Linux 8 Hands-on Lab](documentation/RHEL8-Workshop.adoc)

