**Templates**
=============

About Templates
---------------

Templates define the customizable blueprints for how FogLAMP Manage
entities are created and managed. Every Asset, Data Source, Integration,
Connection, and Event Processor is created from a template. The entity
has a live relationship to that template for the entirety of its live;
updates to the template can update the objects created from that
template

Some key functionality offered by the Template management system:

-  Templates provide a mechanism that allows the administrator of the
   templates to create custom blueprints that can be applied
   throughout the set of managed FogLAMPs. This means that entities
   can be tailored to follow in house conventions and limited to
   allowing just those items that need to differ to be accessible.
   The full configuration of a plugin is no longer offered to the
   user and the process is simplified and enforcement of local
   policies can be applied.

-  New templates may be created from a blank starting point or may be
   created based on an existing template. The latter will inherit
   from the base template it was created from and maintains the same
   type of live link to its parent template as an entity does to the
   template it was created from.

-  Existing Templates can be modified, changing the functionality of
   existing entities within the version.

-  Templates that are not in use in the active version can be deleted,
   removing it from the version.

-  Templates that are in use in the active version can be deprecated.
   Deprecating a Template prevents new entities from being created
   using the Template while keeping the existing instances of the
   Templates.

A Template is a definition of both the optional software packages and
properties required to create an instance of the entity. The properties
defined can dictate how the software, if any, gets configured and how
the entity interacts with other entities in the Data Flow.

FogLAMP Manage Templates use JSON formatting. JSON by nature does not
require a strict ordering of fields in its definitions. This means that
when defining Templates, there is no specific ordering that must be
followed. However, for human interpretability, it is recommended that a
consistent ordering is used.

Templates are versioned as a part of the FogLAMP Manage versioning
system. Templates must be added or modified within unlocked versions, as
once a version has been deployed it is locked to preserve the
configuration.

The sections below will cover everything you need to know about
Templates. You will learn how to use the various elements of a Template
to form a complete template definition for each type of FogLAMP Manage
entity.

Elements of a Template
----------------------

+-----------------+-----------------+-----------------+-----------------+
| **Name**        | **Type**        | **Description** | **Example**     |
+=================+=================+=================+=================+
| name            | string          | The name of the | HTTPS           |
|                 |                 | template. This  |                 |
|                 |                 | must be a       |                 |
|                 |                 | unique name for |                 |
|                 |                 | the template;   |                 |
|                 |                 | no other        |                 |
|                 |                 | template can    |                 |
|                 |                 | have this name. |                 |
+-----------------+-----------------+-----------------+-----------------+
| type            | string          | The type of the | connection      |
|                 |                 | template; this  |                 |
|                 |                 | defines what    |                 |
|                 |                 | type of entity  |                 |
|                 |                 | the template    |                 |
|                 |                 | applies to. See |                 |
|                 |                 | `Template       |                 |
|                 |                 | Types <https:// |                 |
|                 |                 | docs.google.com |                 |
|                 |                 | /document/d/1Eg |                 |
|                 |                 | mlvLA2l1SQfOqHB |                 |
|                 |                 | tZJ-cK3nuKFTkQU |                 |
|                 |                 | Y93iyycuA1g/edi |                 |
|                 |                 | t#heading=h.4oz |                 |
|                 |                 | cnvjuhnd6>`__   |                 |
|                 |                 | for a fuller    |                 |
|                 |                 | description of  |                 |
|                 |                 | template types. |                 |
+-----------------+-----------------+-----------------+-----------------+
| srcType         | string          | Only valid for  | FogLAMP         |
|                 |                 | templates that  |                 |
|                 |                 | create          |                 |
|                 |                 | connections.    |                 |
|                 |                 | The type of the |                 |
|                 |                 | source entity   |                 |
|                 |                 | for this        |                 |
|                 |                 | connection. See |                 |
|                 |                 | `Connection     |                 |
|                 |                 | Type            |                 |
|                 |                 | Templates <http |                 |
|                 |                 | s://docs.google |                 |
|                 |                 | .com/document/d |                 |
|                 |                 | /1EgmlvLA2l1SQf |                 |
|                 |                 | OqHBtZJ-cK3nuKF |                 |
|                 |                 | TkQUY93iyycuA1g |                 |
|                 |                 | /edit#heading=h |                 |
|                 |                 | .qxxmqy5x1oci>` |                 |
|                 |                 | __              |                 |
+-----------------+-----------------+-----------------+-----------------+
| destType        | string          | Only valid for  | FogLAMP         |
|                 |                 | templates that  |                 |
|                 |                 | create          |                 |
|                 |                 | connections.    |                 |
|                 |                 | The type of the |                 |
|                 |                 | destination     |                 |
|                 |                 | entity for this |                 |
|                 |                 | connection. See |                 |
|                 |                 | `Connection     |                 |
|                 |                 | Type            |                 |
|                 |                 | Templates <http |                 |
|                 |                 | s://docs.google |                 |
|                 |                 | .com/document/d |                 |
|                 |                 | /1EgmlvLA2l1SQf |                 |
|                 |                 | OqHBtZJ-cK3nuKF |                 |
|                 |                 | TkQUY93iyycuA1g |                 |
|                 |                 | /edit#heading=h |                 |
|                 |                 | .qxxmqy5x1oci>` |                 |
|                 |                 | __              |                 |
+-----------------+-----------------+-----------------+-----------------+
| validSrc        | array           | List of         | [ "FlirAX8" ]   |
|                 |                 | templates that  |                 |
|                 |                 | may be the      |                 |
|                 |                 | source for a    |                 |
|                 |                 | connection      |                 |
|                 |                 | template. See   |                 |
|                 |                 | `Connection     |                 |
|                 |                 | Type            |                 |
|                 |                 | Templates <#con |                 |
|                 |                 | nection-type-te |                 |
|                 |                 | mplates>`__     |                 |
+-----------------+-----------------+-----------------+-----------------+
| validDst        | array           | List of         | [ "PI Server" ] |
|                 |                 | templates that  |                 |
|                 |                 | may be the      |                 |
|                 |                 | destination of  |                 |
|                 |                 | a connection    |                 |
|                 |                 | template. See   |                 |
|                 |                 | `Connection     |                 |
|                 |                 | Type            |                 |
|                 |                 | Templates <#con |                 |
|                 |                 | nection-type-te |                 |
|                 |                 | mplates>`__     |                 |
+-----------------+-----------------+-----------------+-----------------+
| filters         | array           | List of Filters | [               |
|                 |                 | to be embedded  | "FilrValidity"  |
|                 |                 | into the        | ]               |
|                 |                 | Template. When  |                 |
|                 |                 | an entity is    |                 |
|                 |                 | created using a |                 |
|                 |                 | Template, a     |                 |
|                 |                 | Filter will     |                 |
|                 |                 | automatically   |                 |
|                 |                 | be created for  |                 |
|                 |                 | each Filter     |                 |
|                 |                 | defined in      |                 |
|                 |                 | “filters”. See  |                 |
|                 |                 | `Defining       |                 |
|                 |                 | Filters in a    |                 |
|                 |                 | Template <#defi |                 |
|                 |                 | ning-filters-in |                 |
|                 |                 | -a-template>`__ |                 |
+-----------------+-----------------+-----------------+-----------------+
| owner           | string          | The user that   | system          |
|                 |                 | created the     |                 |
|                 |                 | template, or    |                 |
|                 |                 | "system" if it  |                 |
|                 |                 | was a template  |                 |
|                 |                 | delivered with  |                 |
|                 |                 | the system. See |                 |
|                 |                 | `Template       |                 |
|                 |                 | Ownership &     |                 |
|                 |                 | Rights <#templa |                 |
|                 |                 | te-properties>` |                 |
|                 |                 | __              |                 |
+-----------------+-----------------+-----------------+-----------------+
| rights          | Object          | The set of      |                 |
|                 |                 | access rights   |                 |
|                 |                 | open to users   |                 |
|                 |                 | other than the  |                 |
|                 |                 | owner of this   |                 |
|                 |                 | template. See   |                 |
|                 |                 | `Template       |                 |
|                 |                 | Ownership &     |                 |
|                 |                 | Rights <#templa |                 |
|                 |                 | te-properties>` |                 |
|                 |                 | __              |                 |
+-----------------+-----------------+-----------------+-----------------+
| rights.use      | boolean         | Other users may | true            |
|                 |                 | use this        |                 |
|                 |                 | template to     |                 |
|                 |                 | create          |                 |
|                 |                 | entities.       |                 |
+-----------------+-----------------+-----------------+-----------------+
| rights.inherit  | boolean         | Other users may | true            |
|                 |                 | create          |                 |
|                 |                 | templates that  |                 |
|                 |                 | inherit from    |                 |
|                 |                 | this template.  |                 |
+-----------------+-----------------+-----------------+-----------------+
| rights.update   | boolean         | Other users may | false           |
|                 |                 | update this     |                 |
|                 |                 | template.       |                 |
+-----------------+-----------------+-----------------+-----------------+
| software        | Array           | The set of      |                 |
|                 |                 | software        |                 |
|                 |                 | packages        |                 |
|                 |                 | required by the |                 |
|                 |                 | template. See   |                 |
|                 |                 | `Defining       |                 |
|                 |                 | Software in a   |                 |
|                 |                 | Template <#defi |                 |
|                 |                 | ning-software-i |                 |
|                 |                 | n-a-template>`_ |                 |
|                 |                 | _               |                 |
+-----------------+-----------------+-----------------+-----------------+
| software[].name | string          | The package     | foglamp-source- |
|                 |                 | name of the     | http            |
|                 |                 | software        |                 |
|                 |                 | package         |                 |
|                 |                 | required.       |                 |
+-----------------+-----------------+-----------------+-----------------+
| software[].plu\ | string          | The plugin name | HTTP-South      |
| gin             |                 | of the plugin   |                 |
|                 |                 | to use.         |                 |
+-----------------+-----------------+-----------------+-----------------+
| software[].ver\ | Object          | The version     |                 |
| sion            |                 | constraints for |                 |
|                 |                 | the software    |                 |
|                 |                 | package.        |                 |
+-----------------+-----------------+-----------------+-----------------+
| software[].ver\ | string          | The minimum     | 1.0.3           |
| sion.minimum    |                 | version of the  |                 |
|                 |                 | package that    |                 |
|                 |                 | this template   |                 |
|                 |                 | requires.       |                 |
+-----------------+-----------------+-----------------+-----------------+
| software[].ver\ | string          | An optional     | 1.5.2           |
| sion.maximum    |                 | maximum version |                 |
|                 |                 | that this       |                 |
|                 |                 | template        |                 |
|                 |                 | requires for    |                 |
|                 |                 | the named       |                 |
|                 |                 | software        |                 |
|                 |                 | package. This   |                 |
|                 |                 | may be omitted  |                 |
|                 |                 | in which case   |                 |
|                 |                 | the template    |                 |
|                 |                 | can use any     |                 |
|                 |                 | available       |                 |
|                 |                 | version which   |                 |
|                 |                 | is equal to or  |                 |
|                 |                 | greater than    |                 |
|                 |                 | the version     |                 |
|                 |                 | defined as the  |                 |
|                 |                 | minimum.        |                 |
+-----------------+-----------------+-----------------+-----------------+
| software[].qua\ | string          | Optional. Used  | source          |
| lifier          |                 | for connector   |                 |
|                 |                 | type templates  |                 |
|                 |                 | to indicate if  |                 |
|                 |                 | the software is |                 |
|                 |                 | required on the |                 |
|                 |                 | source or       |                 |
|                 |                 | destination of  |                 |
|                 |                 | the connection. |                 |
+-----------------+-----------------+-----------------+-----------------+
| properties      | Array           | See `Defining   |                 |
|                 |                 | Properties in a |                 |
|                 |                 | Template <#defi |                 |
|                 |                 | ning-properties |                 |
|                 |                 | -in-a-template> |                 |
|                 |                 | `__             |                 |
+-----------------+-----------------+-----------------+-----------------+
| properties[].n\ | string          | The name of the | assetPrefix     |
| ame             |                 | property        |                 |
+-----------------+-----------------+-----------------+-----------------+
| properties[].t\ | string          | Type type of    | string          |
| ype             |                 | the property.   |                 |
|                 |                 | This may be any |                 |
|                 |                 | of the types    |                 |
|                 |                 | defined in      |                 |
|                 |                 | FogLAMP for     |                 |
|                 |                 | configuration   |                 |
|                 |                 | category types  |                 |
|                 |                 | or the          |                 |
|                 |                 | particular      |                 |
|                 |                 | management      |                 |
|                 |                 | types. See      |                 |
|                 |                 | `Property       |                 |
|                 |                 | Types <#propert |                 |
|                 |                 | y-types>`__     |                 |
+-----------------+-----------------+-----------------+-----------------+
| properties[].d\ | string          | The default     | http            |
| efault          |                 | value of the    |                 |
|                 |                 | property. Note  |                 |
|                 |                 | that templates  |                 |
|                 |                 | never define    |                 |
|                 |                 | actual values,  |                 |
|                 |                 | only default    |                 |
|                 |                 | values. This is |                 |
|                 |                 | important to    |                 |
|                 |                 | the way         |                 |
|                 |                 | `inheritance <h |                 |
|                 |                 | ttps://docs.goo |                 |
|                 |                 | gle.com/documen |                 |
|                 |                 | t/d/1EgmlvLA2l1 |                 |
|                 |                 | SQfOqHBtZJ-cK3n |                 |
|                 |                 | uKFTkQUY93iyycu |                 |
|                 |                 | A1g/edit#headin |                 |
|                 |                 | g=h.805g4yctwxz |                 |
|                 |                 | y>`__           |                 |
|                 |                 | works within    |                 |
|                 |                 | templates.      |                 |
+-----------------+-----------------+-----------------+-----------------+
| properties[].d\ | string          | A human         | Asset Name      |
| isplayName      |                 | readable        | Prefix          |
|                 |                 | display name    |                 |
|                 |                 | for use in user |                 |
|                 |                 | interfaces.     |                 |
+-----------------+-----------------+-----------------+-----------------+
| properties[].d\ | string          | A human         | The Asset Name  |
| escription      |                 | readable        | to use for data |
|                 |                 | description of  | ingested on     |
|                 |                 | the property.   | this            |
|                 |                 |                 | connection.     |
+-----------------+-----------------+-----------------+-----------------+
| properties[].o\ | Array           | Only used if    | ["Option 1",    |
| ptions          |                 | properties.type | "Option 2"]     |
|                 |                 | is enumeration. |                 |
|                 |                 | A list of the   |                 |
|                 |                 | options that    |                 |
|                 |                 | should appear   |                 |
|                 |                 | in the dropdown |                 |
|                 |                 | menu.           |                 |
+-----------------+-----------------+-----------------+-----------------+
| properties[].o\ | integer         | An order to use | 2               |
| rder            |                 | when building a |                 |
|                 |                 | UI to display   |                 |
|                 |                 | the properties. |                 |
+-----------------+-----------------+-----------------+-----------------+
| properties[].i\ | boolean         | A flag that can | false           |
| mmutable        |                 | prevent users   |                 |
|                 |                 | of the template |                 |
|                 |                 | from entering   |                 |
|                 |                 | values other    |                 |
|                 |                 | than the        |                 |
|                 |                 | default given   |                 |
|                 |                 | in this         |                 |
|                 |                 | template.       |                 |
+-----------------+-----------------+-----------------+-----------------+
| properties[].q\ | string          | Used in         | destination     |
| ualifier        |                 | connection type |                 |
|                 |                 | templates to    |                 |
|                 |                 | allow the       |                 |
|                 |                 | property to be  |                 |
|                 |                 | associated with |                 |
|                 |                 | the source or   |                 |
|                 |                 | the             |                 |
|                 |                 | destination.    |                 |
+-----------------+-----------------+-----------------+-----------------+

.. _template-types-1:

Template Types
--------------

FogLAMP Manage supports a number of different templates types;

-  **Asset -** Asset Templates describe the items being monitored in the
   logical model that is manipulated by the FogLAMP Manage.

-  **Data Source -** Data Source Templates represent external sensors or
   data collection devices.

-  **Integration -** Integration Templates model the systems north of
   FogLAMP that receive the data from FogLAMP. This may be the cloud
   services or the on premise data historians into which data is
   processed from FogLAMP.

-  **Connection -** Connection Templates describe how elements in the
   logical model are connected together.

-  **Filter -** Filter Templates are a base template for defining a
   single filter that can be applied to a Connection or embedded into
   another entity. It defines the processing elements that may be
   applied to the data as it traverses the connection.

-  **Event Processor -** Event Processor Templates provide the template
   for defining the rules to evaluate on the data and the mechanism
   for delivering Event Processors when those rules trigger.

Asset Type Templates
~~~~~~~~~~~~~~~~~~~~

About Asset Templates
^^^^^^^^^^^^^^^^^^^^^

An Asset Template is used to create an instance of an Asset. For
information on what an Asset is, see the `Assets <#assets>`__ section.

Asset Template Skeleton
^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: JSON

    {
        "name": "YOUR_ASSET_NAME",
        "type": "Asset",
        "software": [],
        "properties": [],
        "filters": [],
        "owner": "System",
        "rights": {"inherit": true, "update": true, "use": true}
    }

The core configuration elements in the definition of an Asset Template
are;

-  `Software <#defining-software-in-a-template>`__

-  `Properties <#defining-properties-in-a-template>`__

-  `Filters <#defining-filters-in-a-template>`__

For information on these fields and how to configure them, see the
linked sections.

Example
^^^^^^^

Suppose you work in a factory that contains several pumps that are prone
to overheating. You would like to monitor the temperature of these pumps
so that you can make informed decisions about how to avoid the
overheating. In this case, the Asset that you are monitoring would be a
pump.

Below depicts an example of what an Asset Template for a pump might look
like.

.. code-block:: JSON

    {
        "name": "Pump",
        "type": "Asset",
        "software": [],
        "properties": [],
        "filters": [],
        "owner": "System",
        "rights": {"inherit": true, "update": true, "use": true}
    }

When creating an Asset using the "Pump" Template, you will see the
following form:

|image20|

Data Source Type Templates
~~~~~~~~~~~~~~~~~~~~~~~~~~

About Data Source Templates
^^^^^^^^^^^^^^^^^^^^^^^^^^^

A Data Source Template is used to create an instance of a Data Source.
For information on what a Data Source is, see the `Data
Sources <#data-sources>`__ section.

Data Source Template Skeleton
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: JSON

    {
        "name": "YOUR_DATASOURCE_NAME",
        "type": "DataSource",
        "software": [],
        "properties": [],
        "filters": [],
        "owner": "System",
        "rights": {"inherit": true, "update": true, "use": true}
    }

The core configuration elements in the definition of a Data Source
Template are;

-  `Software <#defining-software-in-a-template>`__

-  `Properties <#defining-properties-in-a-template>`__

-  `Filters <#defining-filters-in-a-template>`__

For information on these fields and how to configure them, see the
linked sections.

.. _example-1:

Example
^^^^^^^

Building off of the example started in the Asset Templates section.
Suppose you choose to deploy several Flir AX8 thermal cameras to closely
monitor the temperatures of your valuable pump Assets. These Flir AX8s
are by definition Data Source, as they generate data pertaining to your
Assets that are being monitored.

Below depicts an example of what the Data Source Template for a Flir AX8
might look like. The template defines both software required to connect
to a Flir AX8 camera and the properties used to configure the software.
The defined software, or FogLAMP plugin, is foglamp-south-flirax8. The
defined properties "address", "port", "slave", and "timeout" are the
properties used to configure the foglamp-south-flirax8 software.

.. code-block:: JSON

    {
        "name": "flirax8",
        "type": "DataSource",
        "software": [
            {
                "description": "A Modbus connected Flir AX8 thermal imaging camera",
                "package": "foglamp-south-flirax8",
                "plugin": "FlirAX8",
                "version": {
                    "maximum": "1.9.1",
                    "minimum": "1.0.0"
                }
            }
        ],
        "properties": [
            {
                "default": "$Name$",
                "description": "Default asset name",
                "displayName": "Asset Name",
                "immutable": "false",
                "name": "asset",
                "order": "1",
                "type": "string"
            },
            {
                "default": "127.0.0.1",
                "description": "Address of Modbus TCP server",
                "displayName": "Server Address",
                "immutable": "false",
                "name": "address",
                "order": "3",
                "type": "string"
            },
            {
                "default": "502",
                "description": "Port of Modbus TCP server",
                "displayName": "Port",
                "immutable": "false",
                "name": "port",
                "order": "4",
                "type": "integer"
            },
            {
                "default": "1",
                "description": "The Modbus device default slave ID",
                "displayName": "Slave ID",
                "immutable": "false",
                "name": "slave",
                "order": "10",
                "type": "integer"
            },
            {
                "default": "0.5",
                "description": "Modbus request timeout",
                "displayName": "Timeout",
                "immutable": "false",
                "name": "timeout",
                "order": "12",
                "type": "float"
            }
        ],
        "filters": [],
        "owner": "System",
        "rights": {"inherit": true, "update": false, "use": true}
    }

When creating a Data Source using the "flirax8" Template, you will see
the following form:

|image21|

Connection Type Templates
~~~~~~~~~~~~~~~~~~~~~~~~~

About Connection Templates
^^^^^^^^^^^^^^^^^^^^^^^^^^

A Connection Template has a number of optional properties that define
the way the template interacts with the entities at either end of the
connection. Connections are unidirectional, having a source and a
destination. The direction refers to the direction of data flow in the
connection.

-  srcType - the type of the source entity for this connection. Valid
   srcTypes include "Asset", "DataSource", and "FogLAMP"

-  dstType - the type of the destination entity for this connection.
   Valid dstTypes include "DataSource", "FogLAMP", and "Integration"

-  validSrc - the list of valid source templates that this connection
   may connect to. If srcType is "FogLAMP" this property should be
   omitted as it is implied by the type.

-  validDst - the list of valid destination templates this connection
   may connect to. If dstType is "FogLAMP" this property should be
   omitted as it is implied by the type.

Connection Template Skeletons
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Asset to Data Source
''''''''''''''''''''

.. code-block:: JSON

    {
        "name": "YOUR_CONNECTION_NAME",
        "type": "Connection",
        "srcType": "Asset",
        "validSrc": [],
        "dstType": "DataSource",
        "validDst": [],
        "software": [],
        "properties": [],
        "filters": [],
        "owner": "System",
        "rights": {"inherit": true, "update": true, "use": true}
    }

In addition to defining the eligible connections, the Connection
Template also allows for definitions of:

-  `Software <#defining-software-in-a-template>`__

-  `Properties <#defining-properties-in-a-template>`__

-  `Filters <#defining-filters-in-a-template>`__

For information on these fields and how to configure them, see the
linked sections.

Asset to FogLAMP
''''''''''''''''

.. code-block:: JSON

    {
        "name": "YOUR_CONNECTION_NAME",
        "type": "Connection",
        "srcType": "Asset",
        "validSrc": [],
        "dstType": "FogLAMP",
        "software": [],
        "properties": [],
        "filters": [],
        "owner": "System",
        "rights": {"inherit": true, "update": true, "use": true}
    }

**Note:** "validDst" is omitted because the defined "dstType" is
"FogLAMP".

In addition to defining the eligible connections, the Connection
Template also allows for definitions of:

-  `Software <#defining-software-in-a-template>`__

-  `Properties <#defining-properties-in-a-template>`__

-  `Filters <#defining-filters-in-a-template>`__

For information on these fields and how to configure them, see the
linked sections.

Data Source to FogLAMP
''''''''''''''''''''''

.. code-block:: JSON

    {
        "name": "YOUR_CONNECTION_NAME",
        "type": "Connection",
        "srcType": "DataSource",
        "validSrc": [],
        "dstType": "FogLAMP",
        "software": [],
        "properties": [],
        "filters": [],
        "owner": "System",
        "rights": {"inherit": true, "update": true, "use": true}
    }

**Note:** "validDst" is omitted because the defined "dstType" is
"FogLAMP".

In addition to defining the eligible connections, the Connection
Template also allows for definitions of:

-  `Software <#defining-software-in-a-template>`__

-  `Properties <#defining-properties-in-a-template>`__

-  `Filters <#defining-filters-in-a-template>`__

For information on these fields and how to configure them, see the
linked sections.

FogLAMP to Integration
''''''''''''''''''''''

.. code-block:: JSON

    {
        "name": "YOUR_CONNECTION_NAME",
        "type": "Connection",
        "srcType": "FogLAMP",
        "dstType": "Integration",
        "validDst": [],
        "software": [],
        "properties": [],
        "filters": [],
        "owner": "System",
        "rights": {"inherit": true, "update": true, "use": true}
    }

**Note:** "validSrc" is omitted because the defined "srcType" is
"FogLAMP".

In addition to defining the eligible connections, the Connection
Template also allows for definitions of:

-  `Software <#defining-software-in-a-template>`__

-  `Properties <#defining-properties-in-a-template>`__

-  `Filters <#defining-filters-in-a-template>`__

For information on these fields and how to configure them, see the
linked sections.

.. _example-2:

Example
^^^^^^^

For example, suppose that you would like to create a Connection Template
that only allows a Flir AX8 Data Source to a FogLAMP. The source of the
data is the Flir AX8 Data Source, making the srcType "DataSource" and
validSrc "flirax8". The destination of the data is a FogLAMP, making the
dstType "FogLAMP". As noted above, when the srcType or dstType is
FogLAMP the validSrc and validDst fields can be omitted.

An example of a simple Connection Template which connects Flir AX8s to
FogLAMPs:

.. code-block:: JSON

    {
        "name" : "Flir AX8 to FogLAMP",
        "type" : "Connection",
        "srcType" : "Asset",
        "validSrc" : [ "flirax8" ],
        "dstType" : "FogLAMP",
        "filters" : [],
        "owner" : "System",
        "rights" : {
        "use" : true,
        "inherit" : true,
        "update" : false
        },
        "version" : "1.0.0",
        "software" : [],
        "properties" : []
    }

Connection type templates can also define software requirements for both
the source and destination entities, or just for the source or just for
the destination.

The properties of a connection type template define values that are
placed in the configuration of the software that is used to make the
connection. For example if a property X is defined in a connection
template then a value for the plugin that runs that connection will be
created with a name of X.

Also the properties of the template can be tagged with a qualifier of
source, destination or connection to indicate to which end of the
connection the property applies. For example if the property uses a
macro, such as $Name$ then if the qualifier is set to "source", then the
$Name$ part is substituted with the name of the source entity; if the
qualifier is "destination" then the name of the destination entity is
used and likewise for "connection".

A connection template may also be created that allows two FogLAMP
instances to be connected; in this case software is defined for both the
source and destination of the link. The properties are common to both
ends of the connection, i.e. a superset of what is needed on the source
and destination ends and are set in both. The properties have been
omitted from the following example:

.. code-block:: JSON

    {
        "name" : "Interconnection",
        "type" : "Connection",
        "software" : [
            {
                "package" : "foglamp-south-http",
                "version" : {
                    "minimum" : "1.4.0",
                    "maximum" : "1.7.0",
                },
                "qualifier" : "destination"
            },
            {
                "package" : "foglamp-north-http",
                "version" : {
                    "minimum" : "1.4.0",
                    "maximum" : "1.7.0",
                },
                "qualifier" : "source"
            }
        ],
        "properties" : [],
        "srcType" : "FogLAMP",
        "dstType" : "FogLAMP",
        "owner" : "System",
        "rights" : {"use" : true, "inherit" : true, "update" : false}
    }

Integration Templates
~~~~~~~~~~~~~~~~~~~~~

About Integration Templates
^^^^^^^^^^^^^^^^^^^^^^^^^^^

An Integration Template is used to create an instance of an Integration.
For information on what an Integration is, see the `Data
Sources <#data-sources>`__ section.

Integration Template Skeleton
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: JSON

    {
        "name": "YOUR_INTEGRATION_NAME",
        "type": "Integration",
        "software": [],
        "properties": [],
        "filters": [],
        "owner": "System",
        "rights": {"inherit": true, "update": true, "use": true}
    }

The core configuration elements in the definition of an Integration
Template are;

-  `Software <#defining-software-in-a-template>`__

-  `Properties <#defining-properties-in-a-template>`__

-  `Filters <#defining-filters-in-a-template>`__

For information on these fields and how to configure them, see the
linked sections.

Examples
^^^^^^^^

.. code-block:: JSON

    {
        "name": "kafka",
        "type": "Integration",
        "software": [
            {
                "description": "Simple plugin to send data to a Kafka topic",
                "package": "foglamp-north-kafka",
                "plugin": "Kafka",
                "version": {
                    "maximum": "1.9.1",
                    "minimum": "1.0.0"
                }
            }
        ],
        "properties": [
            {
                "default": "localhost:9092,kafka.local:9092",
                "description": "The bootstrap broker list to retrieve full Kafka brokers",
                "displayName": "Bootstrap Brokers",
                "immutable": "false",
                "name": "brokers",
                "order": "1",
                "type": "string"
            },
            {
                "default": "FogLAMP",
                "description": "The topic to send reading data on",
                "displayName": "Kafka Topic",
                "immutable": "false",
                "name": "topic",
                "order": "2",
                "type": "string"
            },
            {
                "default": "readings",
                "description": "The source of data to send",
                "displayName": "Data Source",
                "immutable": "false",
                "name": "source",
                "options": [
                    "readings",
                    "statistics"
                ],
                "order": "3",
                "type": "enumeration"
            }
        ],
        "filters": [],
        "owner": "System",
        "rights": {"inherit": true, "update": false, "use": true},
    }

When creating an Integration using the "kafka" Template, you will see
the following form:

|image22|

Filter Type Templates
~~~~~~~~~~~~~~~~~~~~~

About Filter Templates
^^^^^^^^^^^^^^^^^^^^^^

A Filter Template defines both the plugin and properties used to create
a Filter. For information on what a Filter is, see the
`Filters <#filters>`__ section.

When designing Filter Templates it is important to stay cognisant of
whether you are defining a Filter to be used as an ad hoc or embedded
filter. Below you will find a brief description of each method for
adding a Filter.

First, Filters can be attached in an ad hoc manner on a Connection
either to a FogLAMP or from a FogLAMP. If the connection is to a FogLAMP
then the Filter is placed in the south service and will be visible in
the South Filter column of the Flows page; if it is from a FogLAMP then
the Filter is placed in the north service and will be visible in the
North Filter column of the Flows page.

Second, Filters can be embedded into the Templates of Data Sources,
Connections, and Integrations. When a Filter is embedded into the
Template of another entity, creating an instance of that entity will
also insert the filter into the pipeline created with the Template. An
embedded Filter is considered to be part of the entity it is embedded
in, meaning embedded Filters do not appear as discrete Filters within
Data Flows and are not seen within the South Filter and North Filter
columns of the Flows page.

Filter Template Skeleton
^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: JSON

    {
        "name": "YOUR_FILTER_NAME",
        "type": "FILTER",
        "software": [],
        "properties": [],
        "owner": "System",
        "rights": {"inherit": true, "update": true, "use": true}
    }

The core configuration elements in the definition of an Integration
Template are;

-  `Software <#defining-software-in-a-template>`__

-  `Properties <#defining-properties-in-a-template>`__

For information on these fields and how to configure them, see the
linked sections.

.. _example-3:

Example
^^^^^^^

Building on the example of valuable pump Assets with Flir AX8 Data
Sources, suppose that you require the temperature data to be represented
in Celsius rather than the default unit of Kelvin. We can define a
Filter Template that can be incorporated into the Data Flows to perform
this data conversion.

.. code-block:: JSON

    {
        "name": "expression-filter",
        "type": "Filter",
        "software": [
            {
                "description": "Apply an expression to the data stream",
                "package": "foglamp-filter-expression",
                "plugin": "expression",
                "version": {
                    "maximum": "1.9.1",
                    "minimum": "1.4.0"
                }
            }
        ],
        "properties": [
            {
                "default": "false",
                "description": "A switch that can be used to enable or disable execution
                of the scale filter.",
                "displayName": "Enabled",
                "immutable": "false",
                "name": "enable",
                "order": "1",
                "type": "boolean"
            },
            {
                "default": "log(x)",
                "description": "Expression to apply",
                "displayName": "Expression to apply",
                "immutable": "false",
                "name": "expression",
                "order": "2",
                "type": "string"
            },
            {
                "default": "calculated",
                "description": "The name of the new data point",
                "displayName": "Datapoint Name",
                "immutable": "false",
                "name": "name",
                "order": "3",
                "type": "string"
            }
        ],
        "owner": "System",
        "rights": {"inherit": true, "update": false, "use": true}
    }

When attaching an ad hoc Filter using the "expression-filter" Template,
you will see the following form:

|image23|

Event Processor Type Templates
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

About Event Processor Templates
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

An Event Processor Template contains all the information required to set
up an Event Processor; this includes the rule, the software and
properties of the rule, the delivery method(s), and the software and
properties of the delivery method(s).

Currently a Template can only support one rule and one delivery
mechanism; however, future FogLAMP Manage versions are expected to
support multiple delivery plugins for a single Event Processor. Because
of this future feature, the delivery element in an Event Processor is an
array rather than a single object.

Event Processor Template Skeleton
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code-block:: JSON

    {
        "name": "YOUR_EVENT_PROCESSOR_NAME",
        "type": "Notification",
        "software": [],
        "properties": [],
        "rule": {
            "plugin": "RULE_PLUGIN_NAME",
            "properties": []
        },
        "delivery": [
            {
                "plugin": "DELIVERY_PLUGIN_NAME",
                "properties": []
            }
        ],
        "owner": "System",
        "rights": {"inherit": true, "update": false, "use": true}
    }

.. _example-4:

Example
^^^^^^^

To complete the example of monitoring the temperatures of your valuable
pump Assets using Flir AX8 Data Sources, we will create a template for
an Event Processor. Below we define the Event Processor Rule to be a
configurable threshold. If the data point that we are monitoring ever
exceeds the threshold, it will trigger the Event Processor Delivery
Mechanism. We define the Delivery Mechanism to be an email notification.
In all, this Event Processor will monitor a data point, if it ever
exceeds the configured threshold value, it will send out an email to the
configured address.

.. code-block:: JSON

    {
        "name": "Threshold to Email",
        "type": "Notification",
        "software": [
            {
                "description": "Generate a notification when datapoint value crosses a
                boundary.",
                "package": "",
                "plugin": "Threshold",
                "version": {
                    "maximum": "1.0.0",
                    "minimum": "0.0.0"
                }
            },
            {
                "description": "Email notification plugin",
                "package": "foglamp-notify-email",
                "plugin": "email",
                "version": {
                    "maximum": "1.9.1",
                    "minimum": "0.0.0"
                    }
            }
        ],
        "properties": [
            {
                "default": "true",
                "description": "A switch that can be used to enable or disable the
                notification",
                "displayName": "Enabled",
                "immutable": "false",
                "name": "enable",
                "order": "1",
                "type": "boolean"
            },
            {
                "default": "one shot",
                "description": "Type of notification",
                "displayName": "Type",
                "immutable": "false",
                "name": "notification_type",
                "options": "[ \\"one shot\", \\"retriggered\", \\"toggled\" ]",
                "order": "2",
                "type": "enumeration"
            },
            {
                "default": "60",
                "description": "Retrigger time in seconds for sending a new
                notification",
                "displayName": "Retrigger Time",
                "immutable": "false",
                "name": "retrigger_time",
                "order": "3",
                "type": "integer"
            }
        ],
        "rule": {
            "plugin": "Threshold",
            "properties": [
                {
                    "default": "",
                    "description": "The asset name for which notifications will be
                    generated.",
                    "displayName": "Asset name",
                    "immutable": "false",
                    "name": "asset",
                    "order": "1",
                    "type": "string"
                },
                {
                    "default": "",
                    "description": "The datapoint within the asset name for which
                    notifications will be generated.",
                    "displayName": "Datapoint name",
                    "immutable": "false",
                    "name": "datapoint",
                    "order": "2",
                    "type": "string"
                },
                {
                    "default": ">",
                    "description": "The condition to evaluate",
                    "displayName": "Condition",
                    "immutable": "false",
                    "name": "condition",
                    "options": "[\">\", \\">=\", \\"<\", \\"<=\"]",
                    "order": "3",
                    "type": "enumeration"
                },
                {
                    "default": "0.0",
                    "description": "Value at which to trigger a notification.",
                    "displayName": "Trigger value",
                    "immutable": "false",
                    "name": "trigger_value",
                    "order": "4",
                    "type": "float"
                },
                {
                    "default": "Single Item",
                    "description": "The rule evaluation data: single item or window",
                    "displayName": "Evaluation data",
                    "immutable": "false",
                    "name": "evaluation_data",
                    "options": "[\"Single Item\", \\"Window\"]",
                    "order": "5",
                    "type": "enumeration"
                },
                {
                    "default": "Average",
                    "description": "Window data evaluation type",
                    "displayName": "Window evaluation",
                    "immutable": "false",
                    "name": "window_data",
                    "options": "[\"Maximum\", \\"Minimum\", \\"Average\"]",
                    "order": "6",
                    "type": "enumeration",
                    "validity": "evaluation_data != \\"Single Item\""
                },
                {
                    "default": "30",
                    "description": "Duration of the time window, in seconds, for collecting
                    data points",
                    "displayName": "Time window",
                    "immutable": "false",
                    "name": "time_window",
                    "order": "7",
                    "type": "integer",
                    "validity": "evaluation_data != \\"Single Item\""
                }
            ]
        },
        "delivery": [
            {
                "plugin": "email",
                "properties": [
                    {
                        "default": "alert.subscriber@dianomic.com",
                        "description": "The address to send the alert to",
                        "displayName": "To address",
                        "immutable": "false",
                        "name": "email_to",
                        "order": "1",
                        "type": "string"
                    },
                    {
                        "default": "Notification alert subscriber",
                        "description": "The name to send the alert to",
                        "displayName": "To ",
                        "immutable": "false",
                        "name": "email_to_name",
                        "order": "2",
                        "type": "string"
                    },
                    {
                        "default": "FogLAMP alert notification",
                        "description": "The email subject",
                        "displayName": "Subject",
                        "immutable": "false",
                        "name": "subject",
                        "order": "3",
                        "type": "string"
                    },
                    {
                        "default": "dianomic.alerts@gmail.com",
                        "description": "The address the email will come from",
                        "displayName": "From address",
                        "immutable": "false",
                        "name": "email_from",
                        "order": "4",
                        "type": "string"
                    },
                    {
                        "default": "Notification alert",
                        "description": "The name used to send the alert email",
                        "displayName": "From name",
                        "immutable": "false",
                        "name": "email_from_name",
                        "order": "5",
                        "type": "string"
                    },
                    {
                        "default": "smtp.gmail.com",
                        "description": "The SMTP server name/address",
                        "displayName": "SMTP Server",
                        "immutable": "false",
                        "name": "server",
                        "order": "6",
                        "type": "string"
                    },
                    {
                        "default": "587",
                        "description": "The SMTP server port",
                        "displayName": "SMTP Port",
                        "immutable": "false",
                        "name": "port",
                        "order": "7",
                        "type": "integer"
                    },
                    {
                        "default": "true",
                        "description": "Use SSL/TLS for email transfer",
                        "displayName": "SSL/TLS",
                        "immutable": "false",
                        "name": "use_ssl_tls",
                        "order": "8",
                        "type": "boolean"
                    },
                    {
                        "default": "dianomic.alerts@gmail.com",
                        "description": "Email account name",
                        "displayName": "Username",
                        "immutable": "false",
                        "name": "username",
                        "order": "9",
                        "type": "string"
                    },
                    {
                        "default": "pass",
                        "description": "Email account password",
                        "displayName": "Password",
                        "immutable": "false",
                        "name": "password",
                        "order": "10",
                        "type": "string"
                    },
                    {
                        "default": "false",
                        "description": "A switch that can be used to enable or disable execution
                        of the email notification plugin.",
                        "displayName": "Enabled",
                        "immutable": "false",
                        "name": "enable",
                        "order": "11",
                        "type": "boolean"
                    }
                ]
            }
        ],
        "owner": "System",
        "rights": {"inherit": true, "update": false, "use": true}
    }

When creating an Event Processor using the "Threshold to Email"
Template, you will see the following form:

|image24|

Template Software
-----------------

The "software" element of a template describes what software is to be
leveraged by the entity. This tends to be FogLAMP packages, although it
need not be restricted to FogLAMP packages. Each software package may
have version information associated with it, giving a minimum and
optional maximum version that is required in order to use the Template.
When a Template is applied to an entity, such as a FogLAMP instance,
then the required software packages will be installed at the latest
version available within the limits defined in this section.

Connection Templates provide the additional ability to define which end
of the connection the package should be installed. This may result in
software being installed in one or both ends of the connection.

Defining Software in a Template
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The skeleton for the definition of one piece of software is shown below:

.. code-block:: JSON

    {
        "plugin": "",
        "package": "",
        "description": "",
        "version": {
            "maximum": "",
            "minimum": ""
        }
    }

How to configure the elements of a "software" definition:

-  "plugin" - The name of the plugin as seen in FogLAMP and as defined
   in the plugins code

   -  Example: sinusoid

-  "package" - The name of the software package associated with the
   plugin

   -  Example: foglamp-south-sinusoid

-  "description" - A description of what the software does

   -  Example: Sinusoid Poll Plugin which implements sine wave with data
      points

-  "version.minimum" - The minimum version of the software package to be
   installed when an entity is created using the Template

   -  Example: 1.0.0

-  "version.maximum" - The maximum version of the software package to be
   installed when an entity is created using the Template

   -  Example: 2.0.0

An example "software" definition for the sinusoid plugin using the
details from the examples above:

.. code-block:: JSON

    {
        "plugin": "sinusoid",
        "package": "foglamp-south-sinusoid",
        "description": "Sinusoid Poll Plugin which implements sine wave with
        data points",
        "version": {
            "maximum": "2.0.0",
            "minimum": "1.0.0"
        }
    }

Additionally, as shown below, the "software" element of a Template
supports the definition of multiple softwares:

.. code-block:: JSON

    "software": [
        {
            "plugin": "",
            "package": "",
            "description": "",
            "version": {
                "maximum": "",
                "minimum": ""
            }
        },
        {
            "plugin": "",
            "package": "",
            "description": "",
            "version": {
                "maximum": "",
                "minimum": ""
            }
        }
    ]

Template Properties
-------------------

The "properties" element of a Template is used for defining the
properties required to configure the defined software. When using a
Template to create an entity, the way in which the properties are
defined will dictate what information the user must provide.

Defining Properties in a Template
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

The skeleton for the definition of property is shown below:

.. code-block:: JSON

    {
        "name": "",
        "type": "",
        "displayName": "",
        "description": "",
        "default": "",
        "immutable": "",
        "options": "[]",
        "order": ""
    }

How to configure the elements of a "properties" definition:

-  "name" - The name of the property as defined in the software.

   -  Example 1: "stringInput"

   -  Example 2: "optionsInput"

   -  Example 3: "integerInput"

-  "type" - Type type of the property. This may be any of the types
   defined in FogLAMP for configuration category types or the
   particular management types. See the `Property
   Types <#property-types>`__ section below for more information on
   the supported types.

   -  Example 1: "string"

   -  Example 2: "enumeration"

   -  Example 3: "integer"

-  "displayName" - A human readable display name that will appear in the
   UI when configuring the property. The display name should be
   descriptive to help the user understand what value they should
   provide the property with.

   -  Example 1: "String Input"

   -  Example 2: "Options Input"

   -  Example 3: "Integer Input"

-  "description" - A description of what the user should provide as
   input for the property and or what the property is used for when
   configuring the software.

   -  Example 1: "Provide the string value that should be used to
      configure the software"

   -  Example 2: "Provide the option that should be used to configure
      the software"

   -  Example 3: "The immutable integer value that is used to configure
      the software"

-  "default" - The default value of the property. Note that templates
   never define actual values, only default values. If no alternative
   value is provided for the property, then the default value will be
   used.

   -  Example 1: "Default String"

   -  Example 2: "Option 1"

   -  Example 3: "100"

-  "immutable" - A boolean flag that can prevent users of the template
   from entering values other than the default given in this
   template. If immutable is true, then the "default" value will be
   used and the property will not be displayed on the GUI when
   configuring the entity.

   -  Example 1: "false"

   -  Example 2: "false"

   -  Example 3: "true"

-  "options" - Only used if the property "type" is enumeration.
   "options" defines a list of the value options to choose from when
   configuring the entity.

   -  Example 1: property type is not "enumeration" so this property is
      omitted

   -  Example 2: "[ \\"Option 1\", \\"Option 2\", \\"Option 3\" ]"

   -  Example 3: property type is not "enumeration" so this property is
      omitted

-  "order" - The order in which the properties should be displayed when
   configuring the entity in the GUI.

   -  Example 1: "1"

   -  Example 2: "0"

   -  Example 3: "2"

An example "properties" definition using the details from the examples
above:

.. code-block:: JSON

    "properties": [
        {
            "name": "stringInput",
            "type": "string",
            "displayName": "String Input",
            "description": "Provide the string value that should be used to
            configure the software",
            "default": "Default String",
            "immutable": "false",
            "order": "1"
        },
        {
            "name": "optionsInput",
            "type": "enumeration",
            "displayName": "Options Input",
            "description": "Provide the option that should be used to configure the
            software",
            "default": "Option 1",
            "immutable": "false",
            "options": "[ \\"Option 1\", \\"Option 2\", \\"Option 3\" ]",
            "order": "0"
        },
        {
            "name": "integerInput",
            "type": "integer",
            "displayName": "Integer Input",
            "description": "The immutable integer value that is used to configure
            the software",
            "default": "100",
            "immutable": "true",
            "order": "2"
        }
    ]

When adding an entity using a Template with the properties defined
above, the entities configuration page will look as shown below:

|image25|

**Note:** The property "intergerInput" does not appear in this menu,
because immutable was set to true. The default value of 100 will be
used.

Hovering over the property will display the description defined in the
Template:

|image26|

Expanding the Options Input dropdown menu will show all the options
defined in the Template for the enumeration type property:

|image27|

The rules regarding how properties are managed in creation requests are:

1. If a property value is not given in the creation request then the
   value will be taken from the default that is included in the
   template.

2. If no default is given for a property and no value is given in the
   creation request, then an error should be raised.

3. If a property is defined as immutable, then that property must not be
   given in the creation request. An error should be raised if a
   value of that property is passed in the creation request.

4. All values given for properties in the create request should be type
   checked as per the type defined in the property.

Property Types
~~~~~~~~~~~~~~

The property type corresponds to the FogLAMP configuration types, they
may be one of

-  string

-  integer

-  float

-  boolean

-  enumeration

-  IPv4

-  IPv6

-  X509 Certificate

-  Password

-  JSON

-  URL

-  script

In addition, a type of macro may be given. In this case the default is
the name of a macro to execute rather than the actual default. The
Management service has a set of predefined macros that can be used and
also allows the user to define new macros.

Predefined Macros
^^^^^^^^^^^^^^^^^

There are a number of predefined macros shipped with the system.

+-----------------------------------+-----------------------------------+
| **Macro**                         | **Description**                   |
+===================================+===================================+
| $Address$                         | The IP address of the entity.     |
+-----------------------------------+-----------------------------------+
| $SrcAddress$                      | The IP address of the source of   |
|                                   | the connection.                   |
+-----------------------------------+-----------------------------------+
| $DstAddress$                      | The IP address of the destination |
|                                   | of the connection.                |
+-----------------------------------+-----------------------------------+
| $UserPort$                        | A port allocated automatically in |
|                                   | the user port space (i.e. greater |
|                                   | than 1024. The management system  |
|                                   | will track which ports it has     |
|                                   | allocated in each host.           |
+-----------------------------------+-----------------------------------+
| $Name$                            | The name of the entity.           |
+-----------------------------------+-----------------------------------+
| $SrcName$                         | The name of the source entity in  |
|                                   | a connection.                     |
+-----------------------------------+-----------------------------------+
| $DstName$                         | The name of the destination       |
|                                   | entity in a connection.           |
+-----------------------------------+-----------------------------------+
| $Src(\ *name*)$                   | We substitute the value of the    |
|                                   | property *name* from the source   |
|                                   | of the connection. Valid only for |
|                                   | connection templates. E.g. if you |
|                                   | wish to use the Map property from |
|                                   | the source of a connection you    |
|                                   | add the macro $Src(Map)$.         |
+-----------------------------------+-----------------------------------+
| $Dst(\ *name*)$                   | We substitute the value of the    |
|                                   | property *name* from the          |
|                                   | destination of the connection.    |
|                                   | Valid only for connection         |
|                                   | templates.                        |
+-----------------------------------+-----------------------------------+

Macros are used to create configuration entries that relate to data that
is not manually entered into a property value, but rather is derived
from the application of the template within the system definition. For
example, the $SrcAddress$ macro can be replaced with the address of the
source of a connection template. If a connection is between two
FogLAMPs, each will have an address. Rather than hold that address in
multiple locations, it is held with the FogLAMP and when a connection is
made from that FogLAMP, the connection can refer to the address of the
FogLAMP using $SrcAddress$. These macros allow a single change to the
address of the FogLAMP in this case to be propagated to all the places
that require to use the address. The actual macro substitution takes
place at the time of deployment, each time the configuration is
deployed.

Multiple macros, plain text may be mixed with macro calls. For example
if we have a property which is a URL we might have a property default
configured as

   http://$DstAddress$:$UserPort$/foglamp/exchange

This would cause the Management software to allocate a port and set the
URL using the destination address of a connection entity and that
allocated port.

Filter Properties
-----------------

The “filters” property of a Template allows for the definition of
embedded Filters. The input to this property is a list of defined Filter
Templates. Defining multiple Filters will result in a pipeline of
embedded Filters.

When creating an entity using a Template, for each Filter defined in the
“filters” property, a Filter will be created and attached to the entity.
The user will be prompted to provide all of the non immutable properties
required to configure the Filter(s).

Defining Filters in a Template
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

As stated above, the “filters” property of a Template is simply a list
of Filter Templates that are to be created along with the entity. The
examples below will show various simple Asset Templates with defined
“filters”.

Embedding One Filter:

In this first example, we embed one instance of the expression-filter
that ships with FogLAMP Manage into an Asset Template.

The Asset Template:

.. code-block:: JSON

    {
        "name": "generic asset with embedded filter",
        "type": "Asset",
        "software": [],
        "properties": [],
        "filters": [“expression-filter”],
        "owner": "System",
        "rights": {"inherit": true, "update": false, "use": true}
    }

The “expression-filter” Template that is embedded in the Asset Template
above:

.. code-block:: JSON

    {
        "name": "expression-filter",
        "type": "Filter",
        "software": [
            {
                "description": "Apply an expression to the data stream",
                "package": "foglamp-filter-expression",
                "plugin": "expression",
                "version": {
                    "maximum": "1.9.1",
                    "minimum": "1.4.0"
                }
            }
        ],
        "properties": [
            {
                "default": "false",
                "description": "A switch that can be used to enable or disable execution
                of the scale filter.",
                "displayName": "Enabled",
                "immutable": "false",
                "name": "enable",
                "order": "1",
                "type": "boolean"
            },
            {
                "default": "log(x)",
                "description": "Expression to apply",
                "displayName": "Expression to apply",
                "immutable": "false",
                "name": "expression",
                "order": "2",
                "type": "string"
            },
            {
                "default": "calculated",
                "description": "The name of the new data point",
                "displayName": "Datapoint Name",
                "immutable": "false",
                "name": "name",
                "order": "3",
                "type": "string"
            }
        ],
        "owner": "System",
        "rights": {"inherit": true, "update": false, "use": true}
    }

**Note:** The “expression-filter” Template has 3 properties: “enable”,
“expression”, and “name”.

When we create an instance of the Asset, we see the following form:

|image28|

This form requests the three properties that are defined in the
“expression-filter” Template. Once the Asset has been created, we see
the Template defined with the Asset.

|image29|

Embedding Multiple Filters
^^^^^^^^^^^^^^^^^^^^^^^^^^

Multiple Filters can easily be defined in the “filters” property to form
a Filters pipeline. Here we will edit the Asset template defined in the
first example to include two instances of the “expression-filter”.

.. code-block:: JSON

    {
        "name": "generic asset with embedded filter",
        "type": "Asset",
        "software": [],
        "properties": [],
        "filters": [“expression-filter”, “expression-filter”],
        "owner": "System",
        "rights": {"inherit": true, "update": false, "use": true}
    }

Now when we create an instance of this Asset, we will be prompted with
the properties required to configure both Filters. And when the Asset
has been created, we will see that two Filters are attached.

|image30|

|image31|

Embedding Filters With Immutable Properties
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

In this last example, we will embed a Filter that has all of its
properties set to immutable. When all of the properties of an embedded
Filter are set to immutable, then the user will not be prompted to
provide any Filter related properties when the entity is created.

Here we modify the “expression-filter” used in the above examples to
only have immutable properties.

.. code-block:: JSON
    {
        "name": "expression-filter",
        "type": "Filter",
        "software": [
            {
                "description": "Apply an expression to the data stream",
                "package": "foglamp-filter-expression",
                "plugin": "expression",
                "version": {
                    "maximum": "1.9.1",
                    "minimum": "1.4.0"
                }
            }
        ],
        "properties": [
            {
                "default": "true",
                "description": "A switch that can be used to enable or disable execution
                of the scale filter.",
                "displayName": "Enabled",
                "immutable": "true",
                "name": "enable",
                "order": "1",
                "type": "boolean"
            },
            {
                "default": "sin(x)",
                "description": "Expression to apply",
                "displayName": "Expression to apply",
                "immutable": "true",
                "name": "expression",
                "order": "2",
                "type": "string"
            },
            {
                "default": "calculated",
                "description": "The name of the new data point",
                "displayName": "Datapoint Name",
                "immutable": "true",
                "name": "name",
                "order": "3",
                "type": "string"
            }
        ],
        "owner": "System",
        "rights": {"inherit": true, "update": false, "use": true}
    }

Creating an instance of the Asset now shows us the following form:

|image32|

|image33|

Template Ownership & Rights
---------------------------

Each Template is tagged with an owner that created the template. This,
in conjunction with the rights, prevents other users changing the
template, inheriting from it or using it to create entities. In
particular, preventing users from updating templates is important for
system-provided templates in order to allow for those templates to be
updated. If a user updates a system-provided template, then an update of
the management software that involves a system template being updated
would cause data to be lost.

Only the owner of a template can update the template rights.

Templates Page in FogLAMP Manage GUI
------------------------------------

Templates Page Overview
~~~~~~~~~~~~~~~~~~~~~~~

The Templates page provides all the functionality needed to manage your
Templates. All existing Templates for Assets, Data Sources,
Integrations, Connections, Filters, and Event Processors can be seen
within the expandable menus. Here you can add new templates as well as
modify, deprecate, and delete existing templates.

The following information is available on a per Template basis:

-  Template Name - Shows the name of the Template as defined in the
   Template. Clicking this name will bring you to the Templates
   definition.

-  Occurrences - Shows all existing entities that were created using the
   corresponding Template. Clicking on an occurrence will bring you
   to the configuration page of that entity.

-  Owner - The owner of the Template as defined in the Template

-  Rights - The rights for use, update, and inherit as defined in the
   Template

|image34|

Adding a New Template
~~~~~~~~~~~~~~~~~~~~~

Before adding a new Template, review the `Templates <#templates>`__
section of the documentation to ensure you understand the principles of
Template design in FogLAMP Manage. To add a new Template, first check
that you are operating in an unlocked FogLAMP Manage version. Then
navigate to the Templates page and click the **Add Template** button in
the top right. From here you can either choose to design the Template
within the provided input space or click **Choose File** to select a
prewritten JSON Template saved on your device. The GUI’s editor will
enforce JSON formatting to mitigate errors. Once finished, click
**Save** to complete the process of adding a new Template.

|image35|

Modifying a Template
~~~~~~~~~~~~~~~~~~~~

Before modifying Template, review the `Templates <#templates>`__ section
of the documentation to ensure you understand the principles of Template
design in FogLAMP Manage. To modify a template, first check that you are
operating in an unlocked FogLAMP Manage version. Then navigate to the
Templates page and select the Template you wish to modify. Here you have
the ability to edit the Templates definition from the GUI. The GUI’s
editor will enforce JSON formatting to mitigate errors. Make any desired
changes and click **Save** to complete the modification of the Template.

Deleting a Template
~~~~~~~~~~~~~~~~~~~

To delete a Template, first check that you are operating in an unlocked
FogLAMP Manage Version. Then navigate to the Templates page and click
the ⋮ button to the right the Template that you wish to delete. Only a
Template with no existing occurrences is eligible for being deleted. If
there are existing occurrences you must either delete the occurrences to
proceed with the deletion, or opt to
`deprecate <#deprecating-a-template>`__ the Template rather than
deleting it. Select **Delete** from the menu. Finally, a confirmation
box will appear asking to confirm the deletion, click **Confirm**.

Deprecating a Template
~~~~~~~~~~~~~~~~~~~~~~

To deprecate a Template, first check that you are operating in an
unlocked FogLAMP Manage Version. Then navigate to the Templates page and
click the ⋮ button to the right the Template that you wish to deprecate.
A Template can be deprecated regardless of whether or not there are
existing occurrences of the Template. Select **Deprecate** from the
menu. Finally, a confirmation box will appear asking to confirm the
depreciation, click **Confirm**. Deprecating a Template prevents you
from creating new instances of that entity in the future.
