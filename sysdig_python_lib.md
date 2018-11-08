---

copyright:
  years: 2018
lastupdated: "2018-11-05"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}


# Sysdig Python library
{: #sysdig_python_lib}

Use dashboards to monitor your infrastructure, applications, and services. You can use pre-defined dashboards. You can also create custom dashboards through the Web UI or programmatically. You can backup and restore dashboards by using Python scripts.
{:shortdesc}


## Configuring the local environment to run Python scripts
{: #config_env}

Complete the following steps to configure your local environment to run programmatic dashboard tasks:

1. Install the following software:

    * Python 2.x (2.7.x)

    * pip version 1.3 or later. (Note: pip is installed as part of the Python package for version 2.7 and later versions.)

    * Optional: [virtualenv](https://virtualenv.pypa.io/en/stable/installation/)

2. Install the Sysdig Python client. Choose one of the following methods:

    * Install using **pip**. Run the following command: 
    
        ```
        pip install sdcclient
        ```
        {: codeblock}

    * Download [Sysdig Monitor/Secure Python client library [External link icon](../icons/launch-glyph.svg "External link icon")](https://github.com/draios/python-sdc-client){:new_window}. Then, unpack the *.zip* file.

    * Clone the repository. Run the following command:

        ```
        git clone https://github.com/draios/python-sdc-client.git
        ```
        {: codeblock}




2. Configure the Python environment.

    1. Create a directory where you want your python tools to be installed.

        ```
        mkdir -p ~/workingdir/venv 
        ```
        {: codeblock}

    2. Change to the the workspace.

        ```
        sudo virtualenv ~/workingdir/venv
        ```
        {: codeblock}

    3. Configure all Python tools to use this workspace.

        ```
        source ~/workingdir/venv/bin/activate
        ```
        {: codeblock}

    (venv) $  # at this point the prompt reminds us we're in the virtual environment
    (venv) $  pip install .    # install the sdcclient library into the venv

The sdcclient module is now available to Python.

