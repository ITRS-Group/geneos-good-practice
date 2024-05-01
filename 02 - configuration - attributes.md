# Geneos Best Practice - Configuration

## Attributes

Geneos Attributes are labels with values that are used to categorise, group and filter Managed Entities quickly and efficiently. They should always be preferred over using wildcard searches on Managed Entity names. Ensuring their consistent use across your organisation's Geneos monitoring is crucial to making the best use of Geneos.

### Uses

Attributes have 5 general uses:

1. View-path in Active Console

    The View-path in the Active Console allows the user to build their own visualisation hierarchy of their estate. Attribute names are used to identify the levels and their order, while the values are the names of the nodes that appear in the State Tree. Because the Active Console can connect to multiple Gateways at once, the use of the View-path becomes the principal way to merge the Managed Entities from all of the Gateways in a meaningful way.

2. Filtering XPath Targets efficiently

    Geneos uses XPath extensively to select data from the directory.

3. Values passed to Actions and Effects as environment variables

    When the Gateway runs an Action (from a Rule), or an Effect as the result of an Alert, it builds a set of values that contain run-time information about the data item that triggered the Action/Effect, various internal parameters and also all the Attributes that are set on the Managed Entity. For an external executable these are set as OS environment variables and for a shared library they are passed as `name=value` pairs are arguments to the function being called. The Attributes can be used to classify the Action/Effect, to present to a user in the form of a list of values and more.

    ⚠ This use is the reason we strongly recommend not prefixing Attribute names with an underscore, as all the other values passed to the Action/Effect have an underscore prefix.

4. Dashboard automation



5. Managed Entity Configuration Hierarchy


### Sources

Attributes can come from, currently, two sources:

* Gateway Configuration
    * Managed Entities
    * Managed Entity Groups

* Dynamic Entities
    * Mappings


### General

Attributes are simple name/value pairs and only apply to Managed Entities and not to any other level of the Geneos directory. Both the name and value of an Attribute are case-sensitive, so `EXAMPLE`, `Example` and `example` are all different.

We recommend that the names of Attributes should be all CAPITALS and make minimal use of non-alphanumeric characters, even if a wider character set is allowed by the software. Avoid using spaces and the allowed punctuation like dashes, underscores, percentage signs and dots.

The values of each named Attribute can be more general but should be consistent across your estate, e.g. avoid mixing case like `London` and `LONDON` or using different word separators, e.g. `Data Center 1` and `Data-Center-1`. The values should have a semantic meaning and this is enforced though a consistent policy in their definition and use.

With the exception of Dynamic Mappings the value of an Attribute is fixed and cannot be made up of User Variables. This makes sense if you consider it is at the Managed Entity level that User Variables are resolved to their final values before being used by configuration items referenced by the Managed Entity, e.g. within Samplers.

### Attribute Categories

We suggest using attributes that fall into 4 categories:

1. Location - Physical or Logical
2. Technology Stack
3. Organisational
4. Miscellaneous

#### Location

Location Attributes represent a hierarchical way of locating the monitored elements that are encapsulated in a single Managed Entity. In more traditional on-premises deployments these could include the data-centre, the city, country, region etc. In cloud and orchestrated environments this may be the cloud region or availability zone, the organisational tenancy, the cluster or virtual machine instance and so on.

* General

  | Attribute  | Alternatives | Examples               | Description |
  | ---------- | ------------ | ---------------------- | ----------- |
  | `LOCATION` |              |                        |             |
  | `REGION`   |              | `EMEA`, `us-central-1` |             |


* Physical Location Attributes

  | Attribute    | Alternatives       | Examples   | Description |
  | ------------ | ------------------ | ---------- | ----------- |
  | `COUNTRY`    |                    | `France`   |             |
  | `STATE`      |                    | `Illinois` |             |
  | `CITY`       | `TOWN`             | `London`   |             |
  | `DATACENTER` | `DATACENTRE`, `DC` | `Alpha`    |             |

* Logical Location Attributes

  | Attribute    | Alternatives   | Examples                    | Description                             |
  | ------------ | -------------- | --------------------------- | --------------------------------------- |
  | `PLATFORM`   |                | `AWS`, `Azure`, `Rackspace` | This can also be a technology Attribute |
  | `AWS-REGION` | `AZURE-REGION` | `eu-west-2`                 |                                         |
  | `VPC`        |                |                             |                                         |
  | `CLUSTER`    |                | `appCluster1`               |                                         |
  | `NAMESPACE`  |                |                             |                                         |
  | `NODE`       |                |                             |                                         |

#### Technology

Attributes that represent the technology being monitored are less likely to be hierarchical and more represent a multi-dimensional matrix of properties of the monitored elements.

* Attributes

  | Attribute     | Alternatives | Examples | Description |
  | ------------- | ------------ | -------- | ----------- |
  | `PLATFORM`    |              |          |             |
  | `APPLICATION` |              |          |             |
  | `COMPONENT`   |              |          |             |
  | `CATEGORY`    |              |          |             |
  | `OS`          |              |          |             |
  | `DATABASE`    |              |          |             |

#### Organisational

* General

  | Attribute     | Alternatives       | Examples                    | Description |
  | ------------- | ------------------ | --------------------------- | ----------- |
  | `ENVIRONMENT` |                    | `PROD`, `Production`, `DEV` |             |
  | `CMDB-ID`     | `APP-ID`, `SERIAL` |                             |             |

* Owner

  | Attribute       | Alternatives       | Examples | Description |
  | --------------- | ------------------ | -------- | ----------- |
  | `LOB`           | `DIVISION`         |          |             |
  | `BUSINESS-UNIT` |                    |          |             |
  | `DEPARTMENT`    |                    |          |             |
  | `OWNER`         | `CONTACT`, `EMAIL` |          |             |
  | `TEAM`          |                    |          |             |

* User

  | Attribute      | Alternatives | Examples | Description |
  | -------------- | ------------ | -------- | ----------- |
  | `CLIENT`       | `CUSTOMER`   |          |             |
  | `USER`         |              |          |             |
  | `ORGANISATION` | `COMPANY`    |          |             |

#### Miscellaneous

* Functional Attributes

  | Attribute  | Alternatives | Examples | Description |
  | ---------- | ------------ | -------- | ----------- |
  | `INCIDENT` |              | `True`   |             |
  | `SLA`      |              | `2h`     |             |
  |            |              |          |             |

* Suggested Attribute Names

 Name | Example Values | Comment
---------|----------|---------
 `APPLICATION` | `TradeFarm` | C1
 `COMPONENT` | `Database`, `Controller` | C2
 `REGION` | `EMEA`, `APAC` | C3
 `LOCATION` | `London`, `Houston` | C3
 `DATACENTER` | `NYC1`, `LNWest` | C3
 `OWNER` | `John Doe` | C3
 `CONTACT` | `l2team@example.com` | C3
 `ENVIRONMENT` | `PROD`, `DEV` | C3

