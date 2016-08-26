=========================
Setup Port Job Headless
=========================

Port jobs are used for copying datasets that are already on the Socrata
platform. Port jobs allow users with publishing rights to copy both
dataset schemas (metadata and columns) and data (rows). This guide shows
how to setup and run a Port Job using the command line interface.

Step 1: Setup your configuration
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Information about your domain, username, password and app token is
required for all DataSync jobs. Note that the user running the job must
have publisher rights on the dataset. A number of other global settings,
such as logging and emailing preferences can also be configured. Please
refer to the `configuration
guide <../resources/preferences-config.html>`__ to
establish your credentials and preferences.

Step 2: Configure job details
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

For general help using DataSync in headless/command-line mode run:

::

    java -jar <DATASYNC_JAR> --help

To run a job execute the following command, replacing ``<..>`` with the
appropriate values (flags explained below):

::

    java -jar <DATASYNC_JAR> -c <CONFIG FILE> -t PortJob -pm copy_all -pd1 <SOURCE DOMAIN> -pi1 <SOURCE DATASET ID> -pd2 <DESTINATION DOMAIN>  -pdt <TITLE OF NEW DATASET> -pp true

Explanation of flags: ``*`` = required flag

.. raw:: html

   <table>
     <thead>
       <tr>
         <th>

Flag - Short Name

.. raw:: html

   </th>
         <th>

Flag - Long Name

.. raw:: html

   </th>
         <th>

Example Values

.. raw:: html

   </th>
         <th>

Description

.. raw:: html

   </th>
       </tr>
     </thead>
     <tbody>
       <tr>
         <td style='text-align: left;'>

-t \*

.. raw:: html

   </td>
         <td style='text-align: left;'>

--jobType

.. raw:: html

   </td>
         <td style='text-align: left;'>

PortJob

.. raw:: html

   </td>
         <td style='text-align: left;'>

Specifies the type of job to run.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td style='text-align: left;'>

-c

.. raw:: html

   </td>
         <td style='text-align: left;'>

--config

.. raw:: html

   </td>
         <td style='text-align: left;'>

/Users/home/config.json

.. raw:: html

   </td>
         <td style='text-align: left;'>

Points to the config.json file you created in Step 1, if you chose to do
so.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td style='text-align: left;'>

-pm \*

.. raw:: html

   </td>
         <td style='text-align: left;'>

--portMethod

.. raw:: html

   </td>
         <td style='text-align: left;'>

copy\_all

.. raw:: html

   </td>
         <td style='text-align: left;'>

One of copy\_all, copy\_schema or copy\_data

.. raw:: html

   </td>
       </tr>
       <tr>
         <td style='text-align: left;'>

--pd1 \*

.. raw:: html

   </td>
         <td style='text-align: left;'>

--sourceDomain

.. raw:: html

   </td>
         <td style='text-align: left;'>

https://opendata.socrata.com

.. raw:: html

   </td>
         <td style='text-align: left;'>

The scheme and domain to which the source dataset belongs.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td style='text-align: left;'>

-pi1 \*

.. raw:: html

   </td>
         <td style='text-align: left;'>

--sourceDatasetId

.. raw:: html

   </td>
         <td style='text-align: left;'>

m985-ywaw

.. raw:: html

   </td>
         <td style='text-align: left;'>

The dataset identifier of the source dataset.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td style='text-align: left;'>

--pd2 \*

.. raw:: html

   </td>
         <td style='text-align: left;'>

--destinationDomain

.. raw:: html

   </td>
         <td style='text-align: left;'>

https://opendata.socrata.com

.. raw:: html

   </td>
         <td style='text-align: left;'>

The scheme and domain where the destination dataset should be copied.

.. raw:: html

   </td>
       </tr>
       <tr>
         <td style='text-align: left;'>

-pi2

.. raw:: html

   </td>
         <td style='text-align: left;'>

--destinationDatasetId

.. raw:: html

   </td>
         <td style='text-align: left;'>

ax36-bgg2

.. raw:: html

   </td>
         <td style='text-align: left;'>

The dataset identifier of the destination dataset.; only relevant if
choosing copy\_data for the --portMethod

.. raw:: html

   </td>
       </tr>
       <tr>
         <td style='text-align: left;'>

-pdt

.. raw:: html

   </td>
         <td style='text-align: left;'>

--destinationDatasetTitle

.. raw:: html

   </td>
         <td style='text-align: left;'>

"Crimes 2014"

.. raw:: html

   </td>
         <td style='text-align: left;'>

The title to give the destination dataset; only relevant if the
destination set is being created by either choosing copy\_all or
copy\_schema for the --portMethod

.. raw:: html

   </td>
       </tr>
       <tr>
         <td style='text-align: left;'>

-pp

.. raw:: html

   </td>
         <td style='text-align: left;'>

--publishDestinationDataset

.. raw:: html

   </td>
         <td style='text-align: left;'>

true

.. raw:: html

   </td>
         <td style='text-align: left;'>

Set this to true to have the destination dataset published before the
Port Job completes; only relevant if the destination set is being
created by either choosing copy\_all or copy\_schema for the portMethod.
If false, the destination dataset will be left as a working copy (false
is the default value)

.. raw:: html

   </td>
       </tr>
       <tr>
         <td style='text-align: left;'>

-ppm

.. raw:: html

   </td>
         <td style='text-align: left;'>

--portPublishMethod

.. raw:: html

   </td>
         <td style='text-align: left;'>

replace

.. raw:: html

   </td>
         <td style='text-align: left;'>

Specifies the publish method to use (replace or upsert). For details on
the publishing methods refer to Step 5 of the Setup a Port Job (GUI)

.. raw:: html

   </td>
       </tr>
     </tbody>
   </table>

Step 3: Job output
~~~~~~~~~~~~~~~~~~

Information about the status of the job will be output to STDOUT. If the
job runs successfully a ‘Success’ message will be output to STDOUT, the
destination dataset id will be printed out and the program will exit
with a normal status code (0). If there was a problem running the job a
detailed error message will be output to STDERR and the program will
exit with an error status code (1). You can capture the exit code to
configure error handling logic within your ETL process.

Complete example job
~~~~~~~~~~~~~~~~~~~~

::

    java -jar <DATASYNC_JAR> -c config.json -t PortJob -pm copy_schema -pd1 https://opendata.socrata.com -pi1 97wa-y6ff -pd2 https://opendata.socrata.com -pdt ‘Port Job Test Title’ -pp true

config.json contents:

::

    {
        "domain": "https://opendata.socrata.com",
        "username": "publisher@socrata.com",
        "password": "secret_password",
        "appToken": "fPsJQRDYN9KqZOgEZWyjoa1SG",
    }

**Running a previously saved job file (.spj file)**

Simply run:

::

    java -jar <DATASYNC_JAR> <.spj FILE TO RUN>

For example:

::

    java -jar <DATASYNC_JAR> /Users/john/Desktop/business_licenses.spj

**NOTE:** you can also create an .spj file directly (rather than saving
a job using the DataSync UI) which stores the job details in JSON
format. Here is an example:

::

    {
      "portMethod": "copy_all",
      "sourceSiteDomain": "https://louis.demo.socrata.com",
      "sourceSetID": "w8e5-buaa",
      "sinkSiteDomain": "https://louis.demo.socrata.com",
      "sinkSetID": "",
      "publishMethod": "upsert",
      "publishDataset": "publish",
      "portResult": "",
      "jobFilename": "job_saved_v0.3.spj",
      "fileVersionUID": 1,
      "pathToSavedJobFile": "/home/louis/Socrata/Github/datasync/src/test/resources/job_saved_v0.3.spj"
    }

