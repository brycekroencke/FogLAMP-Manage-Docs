   **Data Flows**
==============

What is a Data Flow
-------------------

A Data Flow within FogLAMP Manage allows for the creation and management
of end-to-end intelligent data pipelines. Data Flows dictate how the
South and North services get created for each managed FogLAMP. Data
Flows model data pipelines using abstractions of the common components
used throughout typical IIoT 4.0 use cases: assets, data sources, and
integrations.

The sections below go over each component of a Data Flow in detail.

|image8|
--------

Assets
------

What is an Asset
~~~~~~~~~~~~~~~~

Assets are a vital component of your Industry 4.0 infrastructure, they
are the equipment and facilities that produce value. Assets are
typically expensive and require upkeep. Downtime or damage to an asset
can be quite costly. By monitoring assets, insight and actionable data
can be obtained and used to avoid asset downtimes, perform preemptive
maintenance on the asset, and optimize the efficiency of the asset.

Within FogLAMP Manage Data Flows, *Asset* entities are used to model
real world physical assets\ *.* An *Asset* is not a mandatory component
of a Data Flow; however, they allow for real world use cases to be
modeled digitally in an abstract manner. By creating an *Asset*, your
Data Flow will be more human interpretable and easier to organize.

|image9|

How to add an Asset Using the GUI
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

To add an Asset, navigate to the Flows page. From here there are two
paths that can be taken to initiate the process of creating an Asset.

1. The first, and most direct way to begin creating a new Asset is to
   click the **+ Add Asset** button on the Flows page.

2. The second method is to select an existing Data Source within the
   Flows page. Then within the Data Sources configuration locate and
   click the **Add Connection** button. Finally, in the **Select
   Entity** dropdown, choose **Create New.** This method will
   initiate the creation of a Connection between the existing Data
   Source and the Asset being created.

After completing either of the above methods, the following form will be
presented.

|image10|

Expand the **Choose Template** dropdown and select the Template which
corresponds to the Asset being created. If the desired Template does not
yet exist, see the section titled `Asset
Templates <#asset-type-templates>`__. Once selected, a new form will
load containing information as defined in the selected Template. This
includes details about the software as well as input fields for the
Assets name and defined properties. Give the Asset a meaningful name
that is representative of the physical Asset being monitored. Finally,
fill in the properties as required and click the **Save** button to
complete the creation of the Asset.

**If method two was used**: Complete the Add Connection form (shown
below) to finalize the Connection between the existing Data Source and
the newly created Asset. For a basic Connection, leaving everything as
default and clicking **Save** will suffice. See the sections `Connection
Templates <#connection-type-templates>`__ and
`Connections <#connections>`__ for information about advanced Connection
configurations.

|image11|

Data Sources
------------

What is a Data Source
~~~~~~~~~~~~~~~~~~~~~

A data source in the industrial setting is a device used to produce data
pertaining to one or more assets. The data produced by a data source is
valuable, as it can be leveraged to optimize processes, increase safety,
and perform preemptive maintenance. Some common examples of data sources
include sensors, DAQs, PLCs, REST servers, and MQTT brokers.

Within FogLAMP Manage Data Flows, Data Source entities are used to model
the physical data sources. Data Sources are typically used to produce
data pertaining to your Assets.

|image12|

How to add a Data Source
~~~~~~~~~~~~~~~~~~~~~~~~~

To add a Data Source, navigate to the Flows page. From here there are
two paths that can be taken to initiate the process of creating a Data
Source.

1. The first, and most direct way to begin creating a new Data Source is
   to click the **+ Add Data Source** button on the Flows page.

2. The second method is to select an existing Asset within the Flows
   page. Then within the Assets configuration locate and click the
   **Add Connection** button. Finally, in the **Select Entity**
   dropdown, choose **Create New.** This method will initiate the
   creation of a Connection between the existing Asset and the Data
   Source being created.

After completing either of the above methods, the following form will be
presented.\ |image13|

Provide a meaningful name for the Data Source. Next expand the **Choose
Template** dropdown and select the Template which corresponds to the
Data Source being created. If the desired Template does not yet exist,
see the section titled `Data Source
Templates <#data-source-type-templates>`__. Once selected, a new form
will load containing information as defined in the selected Template.
This includes input fields for defined properties and details about the
software. Fill in the properties as required and click the **Save**
button to complete the creation of the Data Source.

**If method two was used**: To complete the Connection between the
existing Asset and the newly created Data Source complete the Add
Connection form (shown below). For a basic Connection, leaving
everything as default and clicking **Save** will suffice. See the
sections `Connection Templates <#connection-type-templates>`__ and
`Connections <#connections>`__ for information about advanced Connection
configurations.

|image14|

Integrations
------------

What in an Integration
~~~~~~~~~~~~~~~~~~~~~~

Integrations in the industrial setting are centralized external systems
that store and report industrial enterprise data such as data platforms
and cloud services.

Within FogLAMP Manage Data Flows, Integration entities are used to model
the external systems that receive data from FogLAMP. Integrations may be
hosted on premise or in a cloud environment. FogLAMP Manage has
Integrations for all major cloud providers and all major outbound
protocols. Some commonly used Integrations include PI OMF, GCP, MQTT,
and OPCUA.

|image15|

How to add an Integration
~~~~~~~~~~~~~~~~~~~~~~~~~

To begin the creation of an Integration, navigate to the Flows page and
click the **+ Add Integration** button. Provide a meaningful name for
the Integration. Next expand the **Choose Template** dropdown and select
the Template which corresponds to the Integration being created. If the
desired Template does not yet exist, see the section titled `Integration
Templates <#integration-templates>`__ for information on how to create
one. Once selected, a new form will load containing information as
defined in the selected Template. This includes input fields for defined
properties and details about the software. Fill in the properties as
required and click the **Save** button to complete the creation of the
Integration.

Filters
-------

What is a Filter
~~~~~~~~~~~~~~~~

Filters are entities that can be attached to Data Flows to perform
additional processing on data in-flight. Filters can transform readings,
add/subtract readings, and enrich readings with metadata. Several
Filters can be applied to an entity in succession to form a Filter
pipeline. Filters can be as simple as converting Farenheit data to
Celsicus or Filters can be more complex such as running ML inference on
the data stream.

Ad Hoc Filters
^^^^^^^^^^^^^^

One method of incorporating Filters into a Data Flow is to attach Ad Hoc
Filters to Connections to or from FogLAMP. Filters that are added to a
Connection to a FogLAMP are considered as South Filters and are
displayed in the South Filter column of the Flows page. Similarly,
Filters that are attached to a Connection from FogLAMP are considered to
be North Filters and are displayed in the North Filter columns of the
Flows page.

Embedded Filters
^^^^^^^^^^^^^^^^

The second method for adding Filters into a Data Flow is to embed the
Filters directly into the Template of another entity. Filter pipelines
can be embedded into the Templates of Data Sources, Integrations, and
Connections. When Filters are embedded into the Template of another
entity, creating an instance of that entity will also spawn the embedded
Filters defined in the Template. Filters that are embedded into another
entity are considered to be a part of that entity, thus these Filters
will not appear in the South Filters and North Filters columns of the
Flows page.

See the `Filters Template <#filter-type-templates>`__ and `Defining
Filters in a Template <#defining-filters-in-a-template>`__ sections for
more information on custom and embedded Filters.

How to Add a Filter
~~~~~~~~~~~~~~~~~~~~

There are two ways in which Filters can be added to a Data Flow.

1. The first is to attach ad hoc Filters to Connections to and from a
   FogLAMP. To add an ad hoc Filter, navigate to the Flows page and
   select the entity whose connection you would like to add a Filter
   to. In the section titled Connection to FogLAMPs, select **+ Add
   Filter**. Complete the Add Filter form in the same manner that you
   would create any other Entity.

2. The second method is to embed Filters into Template definitions.
   Filter pipelines can be embedded into Connection, Data Source, or
   Integration Templates. For more information on how to embed a
   Filter into a Template, see the section `Filter
   Templates <#filter-type-templates>`__.

Connections
-----------

What is a Connection
~~~~~~~~~~~~~~~~~~~~

Connections in FogLAMP Manage are responsible for connecting two
entities. By connecting together Assets, Data Sources, FogLAMPs, and
Integrations a full Data Flow can be formed. Filters can be added to a
Connection to provide additional processing of data at the Connection
level. See the `Filters <#filters>`__ section for more information.

FogLAMP Manage ships with generic Connection Templates for connecting
any Asset to any Data Source, any Data Source to a FogLAMP, and a
FogLAMP to any Integration.

For more information on custom Connections, see the `Connection
Templates <#connection-type-templates>`__ section.

How to Add a Connection
~~~~~~~~~~~~~~~~~~~~~~~~

To add a Connection, first ensure that you are working in an unlocked
version. Then navigate to the Flows page and select the Asset, Data
Source, or Integration that you would like to form a Connection to or
from.

If you are creating a Connection to a FogLAMP, click the **Connect to
FogLAMP** button. Next choose the FogLAMP that you would like to connect
to from the **FogLAMP** dropdown menu. Once a FogLAMP is selected,
choose the desired Connection Template from the **Connection Template**
dropdown menu. Note, if there exists only one compatible Connection
Template, then it will be preselected from the dropdown menu
automatically. Here you also have the option to add a FIlter to the
Connection or provide a custom name for the Connection. Finally, click
**Save** to finish creating the Connection.

If you are creating a Connection to a new or existing entity other than
a FogLAMP, click either **Connect to Asset** or **Connect to Data
Source**. Next from the dropdown menu, you have the option to connect to
an existing entity, or you can create a new entity to connect to. If you
choose to create a new entity, provide all of the details required to
create the entity and click **Save**. Once an entity is selected, choose
the desired Connection Template from the **Connection Template**
dropdown menu. Note, if there exists only one compatible Connection
Template, then it will be preselected from the dropdown menu
automatically. Here you also have the option to provide a custom name
for the Connection. Finally, click **Save** to finish creating the
Connection.

Sorting Data Flows
------------------

The Data Flows page allows you to group and sort by Assets (default
view), Data Sources, FogLAMPs, and Integrations.

Grouped and Sorted by Assets
~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sorting by Asset gives a view of the Data Flows centered around the
physical assets, enabling the user to see which Data Sources are
monitored for a given Asset, which FogLAMP(s) process that Asset’s data,
and which Integrations they deliver it to.

|image16|

Grouped and Sorted by Data Sources
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sorting by Data Source gives a view focused on the types of data which
are processed by your system. For each Data Source, you can see the
Asset(s) it comes from, the FogLAMP(s) that process it, and the
Integrations the data is delivered to.

.. _section-1:

|image17|
~~~~~~~~~

Grouped and Sorted by FogLAMPs
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sorting by FogLAMP gives a view focused on the FogLAMP systems which are
processing your IIoT data. For each FogLAMP, you can see the Asset(s)
and Data Sources they are monitoring and the Integrations the data is
delivered to.

.. _section-2:

|image18|
~~~~~~~~~

Grouped and Sorted by Integrations
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Sorting by Integration gives a view focused on the final destination of
data in your system. For each Integration, you can see the Asset(s) and
Data Source(s) that are monitored and the FogLAMP(s) that process the
monitored data.

.. _section-3:

|image19|
~~~~~~~~~
