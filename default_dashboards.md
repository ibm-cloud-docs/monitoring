---

copyright:
  years:  2018, 2019
lastupdated: "2019-03-06"

keywords: Sysdig, IBM Cloud, monitoring,  predefined dashboards

subcollection: Sysdig

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


# Predefined dashboards
{: #default_dashboards}
You can choose any of the following pre-defined dashboards to monitor your infrastructure:
{:shortdesc}


## Applications
{: #default_dashboards_applications}

The following table lists the pre-defined dashboards that you can select to monitor your applications and infrastructure components:

| Dashboard Name        | Description                                                            | Usage             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| HTTP Overview         | Use this dashboard to monitor the health of your web server. It shows the load on the server and its ability to service requests in a timely manner. | Use the Number of Requests and Avg/Max Request Time panels to gauge overall busyness of your server. </br>Look for correlations between URLs to find opportunities to enhance performance. </br>Use the Status Codes metric to monitor 4xx and 5xx error codes. |  
| HTTP Top Requests  |  Use this dashboard to monitor the top requested URLs to your web server, such as total number of requests, average and maximum times to service the requests, and the amount of traffic contained in the requests and responses. |   |
| MongoDB  | Use this dashboard to monitor how busy your MongoDB service is, which collections are in highest demand, and which collections have the slowest performance.  |  Find which collections may benefit from query and index performance tuning. |
| MySQL/PostgreSQL  | Use this dashboard to monitor the overall load and performance status of your SQL database transactions. Find out the number of requests and how quickly they are handled.  | Improve performance. For example, monitor the response times for the slowest queries and identify changes that you make to the query or the indexes on the tables.  |
| MySQL/PostgreSQL Top  | Use this dashboard to monitor the top SQL queries. View the number of queries received and the amount of traffic sent and received for the query.   | Find the slowest queries, the queries run most times, queries with high traffic.  |
| Nginx  | Use this dashboard to monitor host resources, http connections, top and slowest URLs, and host response codes. | Identify load-balancing adjustments by monitoring the following metrics: Writing, Reading, Waiting connections, CPU Load by Machine, Network Bytes Activity, Requests per Second </br>Look for pages that could be optimized by looking at the Slowest URLs metric. </br>Find problems by looking at Response Codes.  |
{: caption="Table 1. List of application and infrastructure components pre-defined dashboards" caption-side="top"} 


## Host and container dashboards
{: #default_dashboards_host_container}

The following table lists the pre-defined dashboards that you can use to monitor resource utilization and system activity on your hosts and in your containers:


| Dashboard Name        | Description                                                            | Usage             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| *Container Limits*    | Use this dashboard to view CPU and memory metrics that are relative to the host resources that are allocated to each container. | |
| *File System*         | Use this dashboard to view directory mount points, file system devices, and capacity and usage information for the file systems that are mounted on the instance.  </br>File systems that are remotely mounted are not listed by default. To view data for these file systems, add the following entry **remotefs.enabled = true** to the */opt/draios/bin/dragent.properties* file on each instance. </br>When groups are selected, metrics are averages for similar filesystem mount points.| Find which file systems are filling up and which ones are being underutilized. Sort by *fs.bytes.used*.|
| *Overview by Container* | Use this dashboard to view resource usage statistics such as CPU percentage, memory usage percentage, network bytes total, and file bytes total for containers that run on the selected group or instance.  </br>Use the *Time Travel* feature with the *Compare* function in this view to see historical information. Based on the data, verify if processes are running as expected, are misbehaving, or require more resources. | Find out which containers are consuming lots of resources.  </br>Use the information to determine if an application should be moved to a different host. |
| *Overview by Container Image* | Use this dashboard to get an overview of the size, performance, and limitations of the services that is defined in the container image. | |
| Overview by Host | Use this dashboard to view general resource usage statistics such as CPU percentage, memory usage percentage, network bytes total, number of network connections, file bytes total, disk usage, for a host. </br>You can also use this dashboard to monitor a group of instances. </br>Use the *Time Travel* feature with the *Compare* function in this view to see historical information. Based on the data, verify if processes are running as expected, are misbehaving, or require more resources. | Find out which hosts are being unused or overused within a group of hosts with similar job functions. | 
| Overview by Process | Use this dashboard to view general resource usage statistics such as CPU percentage, memory usage percentage, network bytes total, number of network connections, file bytes total, disk usage, for the top processes on a host. </br>You can also use this dashboard to monitor a group of instances. </br>Use the *Time Travel* feature with the *Compare* function in this view to see historical information. Based on the data, verify if processes are running as expected, are misbehaving, or require more resources. | Find out which processes are consuming lots of resources.  </br>Use the information to determine if an application should be moved to a different host. |
| Sysdig Agent Summary | Use this dashboard to view the number of Sysdig agents that are deployed in your environment and their versions. |  | 
| Top Files | Use this dashboard to view the list of top files. You can see the file name, the total of file bytes, the time spent in file I/O, and the file error count. | Find the top disk consumers when you sort by size. </br>Find the busiest files when you sort by I/O. </br>Identify potential errors monitoring the data in the column *File Error Count*. |
| Top Processes | Use this dashboard to view the list of top processes that run in a host or group of hosts. You can see the process name, its path, and all arguments. </br>Use the filter feature to restrict the processes that are listed. | Find which processes are top consumers in an environment where the same process is spawned multiple times. |
| Top Server Processes | Use this dashboard to view resource consumption for processes identified to be server oriented only (httpd, java, ntpd, etc.). | Find the resource usage for server processes. |
{: caption="Table 2. List of host and container pre-defined dashboards" caption-side="top"} 

## Network
{: #default_dashboards_network}

The following table lists the pre-defined dashboards that you can select to monitor your network connections and activity:

| Dashboard Name        | Description                                                            | Usage             |
|-----------------------|------------------------------------------------------------------------|-------------------|
| Connections Table     | Use this dashboard to view the connections between your instances and remote nodes. Monitor traffic for each connection. | Find the top talkers that consume most network traffic on your network. |
| Overview              |  Use this dashboard to view total network utilization over time by direction, application, process and host.| Identify which resources impact response performance the most. |
| Response Times vs Resource Usage | Use this dashboard to view host resource metrics over time as compared to the host's response time in processing network requests. |  |
| Top Ports             |  Use this dashboard to view incoming, outgoing and total bytes per port as well as showing the number of connections to each port number. |  |
{: caption="Table 3. List of network pre-defined dashboards" caption-side="top"} 



## Service
{: #default_dashboards_service}


The following table lists the pre-defined dashboards that you can use to monitor the performance of your services, even if those services are deployed in orchestrated containers:

| Dashboard Name        | Description                                                            | 
|-----------------------|------------------------------------------------------------------------|
| Overview by Service   | Use this dashboard to view the size, performance, and limitations of services running in the same container image. | 
| Service Overview      | Use this dashboard to view the resource utilization and response times of a single service. | 
{: caption="Table 4. List of service pre-defined dashboards" caption-side="top"} 



## Topology
{: #default_dashboards_topology}

The following table lists the pre-defined dashboards that you can use to monitor the logical dependencies of your application tiers:

| Dashboard Name        | Description                                                            | 
|-----------------------|------------------------------------------------------------------------|
| CPU Usage             | Use this dashboard to monitor the interaction between your host and the rest of your infrastructure.  | 
| Network Traffic       | Use this dashboard to monitor the selected instance's bandwidth usage between local processes and processes on remote nodes. |
| Response Times        | Use this dashboard to monitor the communication and network response metrics between all processes on the selected hosts. </br>Response counts and times are shown in averages down to 1 second granularity.  |
{: caption="Table 5. List of topology pre-defined dashboards" caption-side="top"} 

**Note:** Any of these dashboards show dashed lines and grey boxes for instances that do not have the Sysdig agent installed and for which communication is detected.










