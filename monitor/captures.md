---

copyright:
  years:  2018, 2020
lastupdated: "2020-02-12"

keywords: Sysdig, IBM Cloud, monitoring, captures

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

# Managing captures
{: #captures}

A capture is a trace file that you can generate to analyze what happens in a host during a time frame. For example, you can use it to analyze bottlenecks, or component interactions. In the {{site.data.keyword.mon_full_notm}} service, you can create, explore, download, and delete *captures* for individual nodes. 
{:shortdesc}

For more information, see [Captures](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-captures#captures).


## Creating a capture
{: #captures_create}

You create a capture in the *Explore* view.

Complete the following steps to create a capture file:

1. Navigate to the *EXPLORE* section in the web UI. [Learn more](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-launch#launch).

2. Click the switch host icon ![Switch host icon](images/switch_hosts.png).

3. Select a host or a container.

4. Click the actions icon ![Three dots icon](images/actions.png) and select **Sysdig capture**.

    The *Sysdig Capture* window opens.

5. In the *Sysdig Capture* window, define the following parameters:

    1. In the field *Capture path and name*, enter the name of the capture file. You can leave the default value or modify it. The default name includes the date and the timestamp when the capture is created. 

    2. Set a *Time frame* to specify the number of seconds to gather data. The default capture time is 15 seconds. The maximum capture time is 86400 seconds (24 hours). 

    3. (Optional) Add a filter to restrict the amount of trace information that is collected. 

6. Click **Start capture**. The monitoring agent is signaled to start a capture, and send back the resulting trace file. 

7. Click **Go to captures page** to display the list of captures in the *Captures* section of the web UI. 

The *Captures* page shows a table that lists the capture file name, the host it was retrieved from, the time frame, and the size of the capture. 

The status of a capture file can be any of the following values:
* `Requested`: A file is being generated.
* `Uploaded`:  A file is available for download, and analysis.
* `Error`: A file is not available due to a timeout, data that was never received, or an agent error.



## Deleting a capture
{: #captures_delete}

Complete the following steps to delete a capture file:

1. Navigate to the *CAPTURES* section in the web UI. [Learn more](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-launch#launch).
2. Identify and select the capture file that you want to delete.
3. Click **Delete**.



## Exploring a capture
{: #captures_explore}

Complete the following steps to explore a capture file:

1. Navigate to the *CAPTURES* section in the web UI. [Learn more](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-launch#launch).
2. Identify and select the capture file that contains the data for the host that you want to analyze.
3. Click **EXPLORE**.



## Downloading a capture
{: #captures_download}

Complete the following steps to download a capture file:

1. Navigate to the *CAPTURES* section in the web UI. [Learn more](/docs/Monitoring-with-Sysdig?topic=Monitoring-with-Sysdig-launch#launch).
2. Identify and select the capture file that contains the data that you want to download.
3. Click **DOWNLOAD**.


## Chisels
{: #captures_chisels}

A Sysdig chisel is a script that is written in Lua, a scripting language. You can use it to analyze data in a capture file. 

For more information, see [Chisels User Guide ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://github.com/draios/sysdig/wiki/Chisels-User-Guide){:new_window}.



## Csysdig
{: #captures_csysdig}

Csysdig is an open source tool for Linux that is designed for monitoring and debugging. You can use it to analyze capture files. 

For more information, see the following resources:
* [Csysdig blog ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://sysdig.com/blog/csysdig-explained-visually/){:new_window}
* [Csysdig video ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.youtube.com/watch?v=UJ4wVrbP-Q8){:new_window}


