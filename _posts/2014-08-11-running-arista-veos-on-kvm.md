---
author: slowe
comments: true
date: 2014-08-11 09:00:00+00:00
layout: post
slug: running-arista-veos-on-kvm
title: Running Arista vEOS on KVM
wordpress_id: 3491
categories:
- Tutorial
tags:
- KVM
- Libvirt
- Linux
- Networking
- OVS
- Virtualization
- Interoperability
---

In this post, I'll show you how I got Arista's vEOS software running under KVM to create a virtualized Arista switch. There are a number of other articles that help provide instructions on how to do this, but none of those that I found included the use of [libvirt](http://libvirt.org/) and/or [Open vSwitch (OVS)](http://openvswitch.org/).

In order to run vEOS, you must first obtain a copy of vEOS. I can't provide you with a copy; you'll have to register on the Arista Networks site (see [here](https://www.arista.com/en/login)) in order to gain access to the download. The download consists of two parts:

1. The Aboot ISO, which contains the boot loader

2. The vEOS disk image, provided as a VMware VMDK

Both of these are necessary; you can't get away with just one or the other. Further, although the vEOS disk image is provided as a VMware VMDK, KVM/QEMU is perfectly capable of using the VMDK without any conversion required (this is kind of nice).

One you've downloaded these files, you can use the following libvirt domain XML definition to create a VM for running Arista vEOS (you'd use a command like `virsh define <filename>`).

{% gist lowescott/ca31c88a52284eb12ac2 %}

_(Click [here](https://gist.github.com/lowescott/ca31c88a52284eb12ac2) if you can't see the code block above.)_

There are a few key things to note about this libvirt domain XML:

* Note the boot order; the VM must boot from the Aboot ISO first.

* Both the Aboot ISO as well as the vEOS VMDK are attached to the VM as devices, and you _must_ use an IDE bus. Arista vEOS will refuse to boot if you use a SCSI device, so make sure there are no SCSI devices in the configuration. Pay particular attention to the `type=` parameters that specify the correct disk formats for the ISO (type "raw") and VMDK (type "vmdk").

* For the network interfaces, you'll want to be sure to use the e1000 model.

* This example XML definition includes three different network interfaces. (More are supported; up to 7 interfaces on QEMU/KVM.)

* This XML definition leverages [libvirt integration with OVS][1] so that libvirt automatically attaches VMs to OVS and correctly applies VLAN tagging and trunking configurations. In this case, the network interfaces are attaching to a portgroup called "trunked"; this portgroup [trunks VLANs up to the guest domain][2] (the vEOS VM, in this case). In theory, this should allow the vEOS VM to support VLAN trunk interfaces, although I had some issues making this work as expected and had to drop back to tagged interfaces.

Once you have the guest domain defined, you can start it by using `virsh start <guest domain name>`. The first time it boots, it will take a _long_ time to come up. (A _really_ long time---I watched it for a good 10 minutes before finally giving up and walking away to do something else. It was up when I came back.) According to the documentation I've found, this is because EOS needs to make a backup copy of the flash partition (which in this case is the VMDK disk image). It might be quicker for you, but be prepared for a long first boot just in case.

Once it's up and running, use `virsh vncdisplay` to get the VNC display of the vEOS guest domain, then use a VNC viewer to connect to the guest domain's console. You won't be able to SSH in yet, as all the network interfaces are still unconfigured. At the console, set an IP address on the Management1 interface (which will correspond to the first virtual network interface defined in the libvirt domain XML) and then you should have network connectivity to the switch for the purposes of management. Once you create a username and a password, then you'll be able to SSH into your newly-running Arista vEOS switch. Have fun!

For additional information and context, here are some links to other articles I found on this topic while doing some research:

* [vEOS - Running EOS in a VM](https://eos.arista.com/veos-running-eos-in-a-vm/) (this article provides only limited QEMU/KVM information toward the end)

* [Running vEOS on ESXi 5.5](https://eos.arista.com/running-veos-on-esxi-5-5/)

* [Create a VirtualBox Arista vEOS image from the command line](http://thenetworksherpa.com/create-a-vbox-arista-veos-image-via-command-line/)

* [Building a Virtual Lab with Arista vEOS and VirtualBox](http://www.gad.net/Blog/2012/10/27/building-a-virtual-lab-with-arista-veos-and-virtualbox/)

If you have any questions or need more information, feel free to speak up in the comments below. All courteous comments are welcome!

[1]: {% post_url 2012-11-07-using-vlans-with-ovs-and-libvirt %}
[2]: {% post_url 2013-05-28-vlan-trunking-to-guest-domains-with-open-vswitch %}
