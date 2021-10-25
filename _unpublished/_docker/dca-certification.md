---
title: Linux Namespaces, Control Groups (cgroups) and Containers (LXC)
---
# Linux Namespaces

Namespaces allow resource partitioning so that different set of processes can work with different set of resources.

Following are the namespace types:

* cgroup
* IPC
* Network
* Mount
* PID
* Time
* User
* UTS - Hostname and domain name

### References:

* [namespaces(7) — Linux manual page](https://man7.org/linux/man-pages/man7/namespaces.7.html)
* [Linux Kernel Isolation Features](https://www.vdoo.com/blog/linux-kernel-isolation-features)

# Linux Control Groups

Cgroups is a Linux kernel framwork which allows processes to be organized into hierarchical groups with following functionalities:

* Allocate resources like CPU, memory, disk I/O, network usage for a process or group of processes
* Prioritizing resources for given cgroups
* Managing cgroups
* Monitoring cgroups

This feature started as "process containers" at Google and then merged into Linux kernel mainline in version 2.6.24 as control groups.

### References:

* [Everything You Need to Know about Linux Containers, Part I: Linux Control Groups and Process Isolation](https://www.linuxjournal.com/content/everything-you-need-know-about-linux-containers-part-i-linux-control-groups-and-process)
* [Introduction to Linux Control Groups (Cgroups)](https://sysadmincasts.com/episodes/14-introduction-to-linux-control-groups-cgroups)
* [CGROUPS](https://www.kernel.org/doc/Documentation/cgroup-v1/cgroups.txt)
* [Introduction to Control Groups](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/6/html/resource_management_guide/ch01)

# Linux Containers (LXC)

LXC provide a virtual environment with its own process and network space isolated from the rest of the system.

Compared to virtualization, container share same operating system kernel using process isolation. These are very lightweight compared to virtualization.

### References:

* [Everything You Need to Know about Linux Containers, Part II: Working with Linux Containers (LXC)](https://www.linuxjournal.com/content/everything-you-need-know-about-linux-containers-part-ii-working-linux-containers-lxc)
* [What's a Linux container?](https://www.redhat.com/en/topics/containers/whats-a-linux-container)