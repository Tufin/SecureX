## Overview
Tufin's SecureX integration includes Atomic Actions covering SecureTrack, SecureChange, SecureApp, and SecureCloud.  Each Atomic Action is autonomous, meaning you may install and use the Atomic Actions relevant to your Tufin products and disregard any Atomic Actions which are not applicable.

## Account Key Configuration
##### SecureTrack/SecureChange/SecureApp #####
A single Account Key may be utilized when multiple TOS components (SecureTrack, SecureChange, and SecureApp) share the same credentials.  If the credentials differ between SecureTrack, SecureChange, and SecureApp deployments, different Account Keys should be configured for each.

**Important Account Key Parameters:**

| **Parameter** | **Value** | 
| --- | --- | 
| Account Key Type | HTTP Basic Authentication |
| Username | ST, SC, or SA Username |
| Password | ST, SC, or SA Password |
| Authentication Option | Basic |


##### SecureCloud #####
SecureCloud utilizes an API access key for authentication.  No SecureX Account Key needs to be configured for SecureCloud.  Instead, each SecureCloud Atomic Action contains a variable named "API Access Key" which should be used to store the API access key for your account.  For information on creating an API access key in SecureCloud, please see the following Knowledge Center document: https://forum.tufin.com/support/kc/securecloud/Content/SecureCloud/APIAccessKeys.htm.

## Target Configuration
##### SecureTrack/SecureChange/SecureApp #####
A single Target may be utilized when multiple TOS components (SecureTrack, SecureChange, and SecureApp) share the same hostname/IP and credentials.  If the hostname/IP and/or credentials differ between SecureTrack, SecureChange, and SecureApp deployments, different Targets should be configured for each.

**Important Target Parameters:**

| **Parameter** | **Value** | 
| --- | --- | 
| Target Type | HTTP Endpoint |
| Default Account Keys | ST, SC, or SA Account Key (If configured) |
| Protocol | HTTPS |
| Path | <blank> |
| Disable Server Certificate Validation | Check if required |

##### SecureCloud #####

SecureCloud uses an HTTP Endpoint target to identify your SecureCloud instance.  Please note that an Account Key is not used with this target; instead, the API Access Key is configured in the Atomic Action.  Details are provided in the Account Key Configuration section above.

**Important Target Parameters:**

| **Parameter** | **Value** | 
| --- | --- | 
| Target Type | HTTP Endpoint |
| No Account Keys | True |
| Protocol | HTTPS |
| Host/IPAddress | Your SecureCloud URL (Example: example.securecloud.tufin.io |
| Port | <blank> |
| Path | <blank> |

## Atomic Actions

**SecureTrack**
 
1. Tufin Resolve Objects
 
2. Tufin Search Devices
 
3. Tufin Search Policies
 
4. Tufin Search Topology
 

**SecureChange**
 
5. Tufin Get Change Info
 
6. Tufin Submit FW Change Request
 
7. Tufin Submit Server Decom Request

**SecureApp**
 
8. Tufin Search Applications
 
9. Tufin Search Application Connections

**SecureCloud**
 
10. Tufin SecureCloud - Add Public Cloud Policy
 
11. Tufin SecureCloud - Create Cluster
 
12. Tufin SecureCloud - Create Cluster Policies from Connections
 
13. Tufin SecureCloud - Delete Cluster
 
14. Tufin SecureCloud - Delete Discovered Connections
 
15. Tufin SecureCloud - Get Cluster Install Command
 
16. Tufin SecureCloud - Get Cluster Policies
 
17. Tufin SecureCloud - List Accounts
 
18. Tufin SecureCloud - List Applications
 
19. Tufin SecureCloud - List Assets
 
20. Tufin SecureCloud - List K8S Clusters
 
21. Tufin SecureCloud - List K8S Services for Cluster
 
22. Tufin SecureCloud - List K8S Workloads for Cluster
 
23. Tufin SecureCloud - List Public Cloud Policies


### 1. Tufin Resolve Objects

Resolve IP address to Network Object

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| IP Address | IP Address | Yes | 

##### Output

**Tufin Objects Table**

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| id | String | TOS object ID | 
| uid | String | TOS object UID | 
| display_name | String | Display name of object | 
| implicit | Boolean | Is the object implicit? | 
| ip | String | Object IP address | 
| overrides | String | Object overrides (applicable only for Panorama NG) | 
| class_name | String | Class of object | 
| ip_type | String | IPv4 or IPv6 | 
| type | String | Type of object in TOS | 
| type_on_device | String | Type of object on device | 
| comment | String | Object comment | 
| device_id | Integer | ID of device on which object exists | 
| name | String | Name of object | 
| netmask | String | Netmask of object | 
 
### 2. Tufin Search Devices

Search SecureTrack devices

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| Vendor | Device Vendor | No | 
| Model | Device Model | No | 
| Name | Device Name | No | 
| IP Address | Device IP Address | No | 

##### Output

**Tufin Devices Table**

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| model | String | Device model | 
| name | String | Device name | 
| offline | Boolean | Is the device offline? | 
| topology | Boolean | Is the device included in topology? | 
| virtual_type | String | Virtual type of the device | 
| domain_name | String | TOS domain name | 
| id | String | Device ID | 
| ip | String | Device IP address | 
| latest_revision | String | Latest policy revision ID | 
| module_uid | String | Model UID | 
| vendor | String | Device vendor | 
| context_name | String | Device context name | 
| domain_id | String | TOS domain ID | 

### 3. Tufin Search Policies

Search the policies of all devices managed by Tufin

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| Search | The text format is for a field is fieldname:text for example source:192.168.1.1 or bareword for free text search. See the search info documentation in Securetrack Policy Browser page for more information. | Yes | 
| Max Results Per Device | Maximum number of search results to return, per device (Default: 25) | No |

##### Output

**Tufin Policies Table**

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| destination_service | String | Destination service | 
| device | String | Device on which policy exists | 
| source | String | Source address | 
| source_service | String | Source service | 
| action | String | Policy action | 
| destination | String | Destination address | 

### 4. Tufin Search Topology

Search the Tufin Topology Map

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| Source IP | Source IP Address | Yes | 
| Destination IP | Destination IP Address | Yes | 
| Service | Service (for example, “tcp:80”, or “http") | No | 

##### Output

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| Tufin Topology Is Permitted | Boolean | Is the traffic permitted? | 

**Tufin Topology Table**

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| type | String | Device type | 
| vendor | String | Device vendor | 
| hop | Integer | Hop number | 
| id | Integer | Device ID | 
| name | String | Device name | 

### 5. Tufin Get Change Info

Get information on a SecureChange Ticket

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| Ticket ID | SecureChange ticket ID | Yes | 

##### Output

**Tufin Ticket Table**

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| current_step_name | String | Current ticket step | 
| id | Integer | Ticket ID | 
| requester | String | Ticket requester | 
| requester_id | Integer | Ticket requester ID | 
| status | String | Ticket status | 
| workflow_name | String | Name of workflow used for ticket | 
| comments | String | Ticket comments | 
| domain_name | String | TOS domain of ticket | 
| priority | String | Ticket priority | 
| sla_outcome | String | Outcome of ticket SLA | 
| subject | String | Ticket subject | 

### 6. Tufin Submit FW Change Request

Submit a firewall change request to SecureChange.

**Note:** This action is based on the default firewall change request template included with SecureChange.  If changes are made to this template, changes will be required in the JSON submitted in the `Request Body` of the `Submit Change Request` action.

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| Subject | Ticket subject | Yes | 
| Priority | Ticket priority (acceptable values: `Critical`, `High`, `Normal`, `Low`)  | Yes | 
| Source | Source address | Yes | 
| Destination | Destination address | Yes | 
| Port | Port number | Yes | 
| Protocol | Protocol (acceptable values: `TCP`, `UDP`) | Yes | 
| Action | Policy action (acceptable values: `Accept`, `Drop`, `Remove`)  | Yes | 
| Comment | Comment for change request | No | 

##### Output

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| Success | Boolean | Was the ticket created successfully? | 

### 7. Tufin Submit Server Decom Request

Submit a server decommission request to SecureChange.

**Note:** This action is based on the default server decommission request template included with SecureChange.  If changes are made to this template, changes will be required in the JSON submitted in the `Request Body` of the `Submit Change Request` action.

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| Subject | Ticket subject | Yes | 
| Priority | Ticket priority (acceptable values: `Critical`, `High`, `Normal`, `Low`)  | Yes | 
| IP Address | Server IP address | Yes | 
| Comment | Comment for change request | No | 

##### Output

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| Success | Boolean | Was the ticket created successfully? | 

### 8. Tufin Search Applications

Search SecureApp applications by name

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| Application Name | Application Name | No | 

##### Output

**Tufin Applications Table**

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| modified | String | Last modified date | 
| name | String | Application name | 
| status | String | Applcation status | 
| comment | String | Applicaiton comment | 
| created | String | Created date | 
| decommissioned | Boolean | Is the applcation decommissioned | 
| id | Integer | Application ID | 

### 9. Tufin Search Application Connections

Retrieve the connections for a SecureApp application

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| App ID | Application ID | Yes | 

##### Output

**Tufin Application Connections Table**

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| comment | String | Connection comment | 
| destinations | String | List of connection destinations | 
| external | String | Is the connection external | 
| id | Integer | Connection ID | 
| name | String | Connection name | 
| services | String | List of connection services | 
| source | String | List of connection sources | 
| status | String | Connection status | 

### 10. Tufin SecureCloud - Add Public Cloud Policy

Add a rule to the SecureCloud public cloud policy

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| New Policy | See https://***youraccount***.securecloud.tufin.io/api-documentation/index.html#/Policy/put_api_v1_iris_conf_global_policy for policy formatting requirements | Yes | 

##### Output

No output

### 11. Tufin SecureCloud - Create Cluster

Create a new cluster in SecureCloud

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| Cluster Name | Name of the cluster to be created | Yes | 

##### Output

No output

### 12. Tufin SecureCloud - Create Cluster Policies from Connections

Create or update a cluster policy based on the discovered connections

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| Cluster Name | Name of the cluster | Yes | 
| Namespace | Name of the Namespace | No | 

##### Output

No output

### 13. Tufin SecureCloud - Delete Cluster

Delete a cluster from SecureCloud

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| Cluster Name | Name of the cluster to be deleted | Yes | 

##### Output

No output

### 14. Tufin SecureCloud - Delete Discovered Connections

Delete all newly discovered connections for a cluster

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| Cluster Name | Name of the cluster to delete connections from | Yes | 

##### Output

No output

### 15. Tufin SecureCloud - Get Cluster Install Command

Create a new cluster in SecureCloud

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| Cluster Name | Name of the cluster | Yes | 

##### Output

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| Install Command | String | Bash command to be executed on the cluster to add the cluster to SecureCloud |

### 16. Tufin SecureCloud - Get Cluster Policies

Get the Kubernetes policy defined in SecureCloud as a YAML file

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| Cluster Name | Name of the cluster | Yes | 
| Namespace | Name of the namespace | Yes | 

##### Output

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| Policy YAML | String | Kubernetes policy in YAML |

### 17. Tufin SecureCloud - List Accounts

List all public cloud accounts being managed by SecureCloud

##### Input

No input

##### Output

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| Account Objects JSON | String | See https://***youraccount***.securecloud.tufin.io/api-documentation/index.html#/Accounts/get_api_v1_iris_conf_accounts |

### 18. Tufin SecureCloud - List Applications

List all public cloud applications discovered by SecureCloud

##### Input

No input

##### Output

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| Application Objects JSON | String | See https://***youraccount***.securecloud.tufin.io/api-documentation/index.html#/Applications/get_api_v1_iris_model_cross_account_applications |

### 19. Tufin SecureCloud - List Assets

List all public cloud assets

##### Input

No input

##### Output

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| Asset Objects JSON | String | See https://***youraccount***.securecloud.tufin.io/api-documentation/index.html#/Assets/get_api_v1_iris_model_cross_account_assets |

### 20. Tufin SecureCloud - List K8S Clusters

List all Kubernetes clusters managed in SecureCloud

##### Input

No input

##### Output

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| Cluster Objects JSON | String | See https://***youraccount***.securecloud.tufin.io/api-documentation/index.html#/Cluster%20management/get_api_v1_orca_conf_clusters |

### 21. Tufin SecureCloud - List K8S Services for Cluster

List all the Kubernetes services for a cluster managed in SecureCloud

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| Cluster Name | Name of the cluster | Yes | 

##### Output

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| Service Objects JSON | String | See https://***youraccount***.securecloud.tufin.io/api-documentation/index.html#/Kubernetes%20cluster%20resources/get_api_v1_orca_model_clusters__name__services |

### 22. Tufin SecureCloud - List K8S Workloads for Cluster

List all the Kubernetes workloads for a cluster managed in SecureCloud

##### Input

| **Argument Name** | **Description** | **Required** |
| --- | --- | --- |
| Cluster Name | Name of the cluster | Yes | 

##### Output

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| Workloads Objects JSON | String | See https://***youraccount***.securecloud.tufin.io/api-documentation/index.html#/Kubernetes%20cluster%20resources/get_api_v1_orca_model_clusters__name__workloads |

### 23. Tufin SecureCloud - List Public Cloud Policies

Show the public cloud policy defined in SecureCloud

##### Input

No input

##### Output

| **Name** | **Type** | **Description** |
| --- | --- | --- |
| Policy Objects JSON | String | See https://***youraccount***.securecloud.tufin.io/api-documentation/index.html#/Policy/get_api_v1_iris_conf_global_policy |

## Troubleshooting

Contact Tufin support via the Tufin User Portal, or by going to https://www.tufin.com/support
