---

copyright:
  years:  2018, 2020
lastupdated: "2020-09-15"

keywords: Sysdig, IBM Cloud, monitoring, Sysdig agent, log level

subcollection: Monitoring-with-Sysdig

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}

# Baremetals overview
{: #baremetal_ov}

You can view and analyze the Sysdig agent log file to troubleshoot problems. 
{:shortdesc}

In the *Overview module*, you can check the health, risk, and capacity of your bare metal through metrics that are prioritized by event count and severity and refreshed every 10 minutes.



Hosts Infrastructure Dashboards

| Dashboard | Description | Use Cases |
|-----------|-------------|-----------|
| `Host Resource Usage` | This dashboard shows resource usage statistics, including CPU, file bytes, memory and network bytes, for hosts running within the defined scope. | Use this view to identify when a host is being over or under utilized within a group of hosts with similar job functions. |
| `Disk and File System` | This table view shows directory mount points, file system devices, and capacity and usage information for the file systems mounted on the instance. When groups are selected, metrics are averages for similar filesystem mount points. | Identify which file systems are filling up or being underutilized. |
| `Memory Usage` | Displays the memory and swap usage and page faults. |  |
| `Network Traffic & Bandwidth` | Provides an overview of network traffic in the host, including throughput, queue length, and errors |  |
| `Sysdig Agent Health and Status` | This view reports the number of Sysdig agents deployed in your environment and their versions. | 

Remotely mounted file systems are not listed by default. To enable, add the remotefs = true entry to the /opt/draios/bin/dragent.properties file on each instance.
{: note}

| Metric          | Metric formula                                     | Description |
|-----------------|----------------------------------------------------|------------------------------------|
| `CPU %`         | `avg(timeAvg(cpu.used.percent)) by host.hostName`  | The CPU usage for each host is obtained from /proc, and measured as the sum of the CPU usage of all cores, normalized by dividing by the number of cores. </br>The CPU usage for each host is the sum of cpu.user.percent, cpu.nice.percent, cpu.stolen.percent, and cpu.system.percent. </br>The Linux command top can be used to review these values as well. |
| `Load Average (5m)` | `avg(avg(load.average.5m)) by host.hostName`   | The 5 minute system load average represents the average number of jobs in (1) the CPU run queue or (2) waiting for disk I/O averaged over 5 minutes for all cores. The value should correspond to the third (and last) load average value displayed by the 'uptime' command. |
| `Memory Usage %`| `avg(timeAvg(memory.used.percent)) by host.hostName` | The percentage of physical memory in use. By default, this metric displays the average value for the defined scope. For example, if the scope is set to a group of machines, the metric value will be the average value for the whole group. |
| `Network Bytes Total` | `avg(timeAvg(net.bytes.total)) by host.hostName` | Total network bytes. By default, this metric displays the total value for the defined scope. For example, if the scope is set to a group of machines, the metric value will be the total value for the whole group. </br>total number of bytes sent and received  |
| `Swap Usage %` | `avg(avg(memory.swap.used.percent)) by host.hostName` | The percentage of swap memory used. By default, this metric displays the average value for the defined scope. For example, if the scope is set to a group of machines, the metric value will be the average value for the whole group. |
| `Number of Network Connections` | `avg(timeAvg(net.connection.count.total)) by host.hostName` | The number of currently established connections. </br>This metric is especially useful when segmented by port, process, or protocol. </br>This value may exceed the sum of the inbound and outbound metrics since it represents client and server inter-host connections as well as internal only connections. | 
| `Disk Usage` | `max(avg(fs.used.percent)) by host.hostName, fs.device, fs.mountDir` | The amount of space written by a single container instance. This value is provided by the container engine and is not supported for some versions of CRIO. For example, CRIO-1.15 which is used in Openshift 4.2. crictl stats not showing the size indicates that this feature is not supported. |
| `File IOPS` | `sum(timeAvg(file.iops.total)) by host.hostName` | The number of file read and write operations per second. This metric is calculated by measuring the actual number of read/write requests made by a process. By default, this metric displays the total value for the defined scope. For example, if the scope is set to a group of machines, the metric value will be the total value for the whole group. </br>The value of file.iops.total can differ from the value other tools show, as they are usually based on interpolating this value from the number of bytes read and written to the file system. | 
| `Inodes Usage` | `sum(avg(fs.inodes.used.percent)) by host.hostName, fs.device, fs.mountDir` | The percentage of inodes that are used. |

fs.largest.used.percent
The percentage of filesystem space used by the largest filesystem.
fs.mountDir
The filesystem mount directory.

The inode (index node) is a data structure in a Unix-style file system that describes a file-system object such as a file or a directory. Each inode stores the attributes and disk block locations of the object's data. ... Directories are lists of names assigned to inodes.

I have a disk drive where the inode usage is 100% (using df -i command). However after deleting files substantially, the usage remains 100%.

What's the correct way to do it then?

How is it possible that a disk drive with less disk space usage can have higher Inode usage than disk drive with higher disk space usage?

Is it possible if i zip lot of files would that reduce the used inode count?

It's quite easy for a disk to have a large number of inodes used even if the disk is not very full.

An inode is allocated to a file so, if you have gazillions of files, all 1 byte each, you'll run out of inodes long before you run out of disk.

It's also possible that deleting files will not reduce the inode count if the files have multiple hard links. As I said, inodes belong to the file, not the directory entry. If a file has two directory entries linked to it, deleting one will not free the inode.

Additionally, you can delete a directory entry but, if a running process still has the file open, the inode won't be freed.

My initial advice would be to delete all the files you can, then reboot the box to ensure no processes are left holding the files open.

If you do that and you still have a problem, let us know.

By the way, if you're looking for the directories that contain lots of files, this script may help:

#!/bin/bash
# count_em - count files in all subdirectories under current directory.
echo 'echo $(ls -a "$1" | wc -l) $1' >/tmp/count_em_$$
chmod 700 /tmp/count_em_$$
find . -mount -type d -print0 | xargs -0 -n1 /tmp/count_em_$$ | sort -n
rm -f /tmp/count_em_$$

If you are very unlucky you have used about 100% of all inodes and can't create the scipt. You can check this with df -ih.

Then this bash command may help you:

sudo find . -xdev -type f | cut -d "/" -f 2 | sort | uniq -c | sort -n
And yes, this will take time, but you can locate the directory with the most files.

Try to find if this is an inodes problem with:

df -ih
Try to find root folders with large inodes count:

for i in /*; do echo $i; find $i |wc -l; done
Try to find specific folders:

for i in /src/*; do echo $i; find $i |wc -l; done



uptime
The percentage of time the selected entity or entities was down over the defined time window.

Note
While this metric is a percentage value, the value is presented as an integer between 0 and 1, rather than a percentage between 0% and 100%.


memory.bytes.used
The amount of physical memory currently in use. By default, this metric displays the average value for the defined scope. For example, if the scope is set to a group of machines, the metric value will be the average value for the whole group.

The formula for determining memory.bytes.used is slightly different depending on whether you are examining processes or containers. For containers, the formula is rss+cache-inactive_file. This means that the total amount of page cache memory (inactive_file) is subtracted from the total number of bytes of page cache memory, and the total number of bytes of anonymous and swap cache memory, combined.

Note
This is different to the docker stats approach, and may result in different results.

For processes, the formula is the total value of the size of the resident anonymous memory, the size of the resident file mappings, and the size of the resident shared memory.




