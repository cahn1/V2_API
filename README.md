#DOME9 API#

The Dome9 API enables developers to access Dome9 functionality by an API key.
  This describes resourses are currently in a beta version:

##URL

The url to make the requests is https://api.dome9.com/

##Authorization

The authorization make with an API key, which generate by an [automatic tool](docs/more_words.md), by inserting it as Basic Authentication.
 the "id" is the username and the "API Key Secret" is the password.

##Supported features
 
1. [AWS Security Groups](#aws-security-groups)

2. [AWS Accounts](#aws-accounts)

3. [IP Lists](#ip-lists)





##<a name="aws-security-groups">AWS Security Groups</a>
1. [GET](#aws-security-groups-get)
2. [Create Security Groups](#aws-security-groups-create)
3. [Create Service](#aws-security-groups-create-service)
4. [Overwrite service](#aws-security-groups-overwrite-service)
5. [Delete service](#aws-security-groups-delete-service)
6. [Delete Security Groups](#aws-security-groups-delete-security-groups)

<h3><a name="aws-security-groups-get">GET</a></h3>

The get request pull the entire cloud security groups which attached to Dome9.
ID: if the request is made without the security group id then the entire security groups which attached to dome9 will return.

URL: https://api.dome9.com/CloudSecurityGroup/{id} <br \>
METHOD: GET

####Response:

```json
 {
   "securityGroupId": int,
   "externalId": "string",
   "isProtected": boolean,
   "securityGroupName": "string",
   "vpcId": "string",
   "regionId": "string",
   "cloudAccountId": "string",
   "cloudAccountName": "string",
   "services": {},
   "tags": {}
 }
```

* securityGroupId (integer): The Security Group ID in dome9.
* externalId (string): The Security Group ID in AWS.
* isProtected (boolean, optional): set if it will be in Full Protection or Read Only mode.
* securityGroupName (string, optional): The name of the Security Group.
* description (string, optional): The description of the Security Group.
* vpcId (string, optional): The VPC of the Security Group.
* regionId (string, optional): Can be one of the next regions - 'us_east_1', 'us_west_1', 'eu_west_1', 'ap_southeast_1', 'ap_northeast_1', 'us_west_2', 'sa_east_1', 'az_1_region_a_geo_1', 'az_2_region_a_geo_1', 'az_3_region_a_geo_1', 'ap_southeast_2', 'mellanox_region', 'us_gov_west_1', 'eu_central_1', 'ap_northeast_2'
* cloudAccountId (string, optional): Dome9 Cloud Account ID.
* services (object, optional) - The inbound and outbound services.
* tags (object, optional) - The security groups tags.

<h3><a name="aws-security-groups-create">Create Security Groups</a></h3>
Create a new Security Group on AWS.

URL: https://api.dome9.com/CloudSecurityGroup <br \>
METHOD: POST
BODY:
```json
{
  "isProtected": boolean,
  "securityGroupName": "string",
  "description": "string",
  "vpcId": "string",
  "regionId": "us_east_1",
  "cloudAccountId": "string",
  "cloudAccountName": "string",
  "tags": {}
}
```

####Request parameters

* isProtected (boolean, optional): set if it will be in Full Protection or Read Only mode.
* securityGroupName (string, optional): The name of the Security Group.
* description (string, optional): The description of the Security Group.
* vpcId (string, optional): The VPC of the Security Group.
* regionId (string, optional): Can be one of the next regions - 'us_east_1', 'us_west_1', 'eu_west_1', 'ap_southeast_1', 'ap_northeast_1', 'us_west_2', 'sa_east_1', 'az_1_region_a_geo_1', 'az_2_region_a_geo_1', 'az_3_region_a_geo_1', 'ap_southeast_2', 'mellanox_region', 'us_gov_west_1', 'eu_central_1', 'ap_northeast_2'
* cloudAccountId (string, optional): Dome9 Cloud Account ID.
* services (object, optional)
* tags (object, optional)

<h3><a name="aws-security-groups-create-service">Create Service</a></h3>

Create a new service for Security Group on AWS.

URL: https://api.dome9.com/cloudsecuritygroup/{groupid}/services <br \>
METHOD: POST

note: The groupid in the url can be eithe the internal id or the external id.

BODY:
```json
{
  "name": "string",
  "description": "string",
  "protocolType": "string",
  "port": "string",
  "openForAll": boolean,
  "scope": [
    {
      "type": "string",
      "data": object
    }
  ],
  "inbound": boolean,
  "icmpType": "string"
}
```

####Request parameters

* name (string): The service name.
* description (string, optional): The service description.
* protocolType (string): Can be one od the next protocols - 'HOPOPT', 'ICMP', 'IGMP', 'GGP', 'IPV4', 'ST', 'TCP', 'CBT', 'EGP', 'IGP', 'BBN_RCC_MON', 'NVP2', 'PUP', 'ARGUS', 'EMCON', 'XNET', 'CHAOS', 'UDP', 'MUX', 'DCN_MEAS', 'HMP', 'PRM', 'XNS_IDP', 'TRUNK1', 'TRUNK2', 'LEAF1', 'LEAF2', 'RDP', 'IRTP', 'ISO_TP4', 'NETBLT', 'MFE_NSP', 'MERIT_INP', 'DCCP', 'ThreePC', 'IDPR', 'XTP', 'DDP', 'IDPR_CMTP', 'TPplusplus', 'IL', 'IPV6', 'SDRP', 'IPV6_ROUTE', 'IPV6_FRAG', 'IDRP', 'RSVP', 'GRE', 'DSR', 'BNA', 'ESP', 'AH', 'I_NLSP', 'SWIPE', 'NARP', 'MOBILE', 'TLSP', 'SKIP', 'IPV6_ICMP', 'IPV6_NONXT', 'IPV6_OPTS', 'CFTP', 'SAT_EXPAK', 'KRYPTOLAN', 'RVD', 'IPPC', 'SAT_MON', 'VISA', 'IPCV', 'CPNX', 'CPHB', 'WSN', 'PVP', 'BR_SAT_MON', 'SUN_ND', 'WB_MON', 'WB_EXPAK', 'ISO_IP', 'VMTP', 'SECURE_VMTP', 'VINES', 'TTP', 'NSFNET_IGP', 'DGP', 'TCF', 'EIGRP', 'OSPFIGP', 'SPRITE_RPC', 'LARP', 'MTP', 'AX25', 'IPIP', 'MICP', 'SCC_SP', 'ETHERIP', 'ENCAP', 'GMTP', 'IFMP', 'PNNI', 'PIM', 'ARIS', 'SCPS', 'QNX', 'AN', 'IPCOMP', 'SNP', 'COMPAQ_PEER', 'IPX_IN_IP', 'VRRP', 'PGM', 'L2TP', 'DDX', 'IATP', 'STP', 'SRP', 'UTI', 'SMP', 'SM', 'PTP', 'ISIS', 'FIRE', 'CRTP', 'CRUDP', 'SSCOPMCE', 'IPLT', 'SPS', 'PIPE', 'SCTP', 'FC', 'RSVP_E2E_IGNORE', 'MOBILITY_HEADER', 'UDPLITE', 'MPLS_IN_IP', 'MANET', 'HIP', 'SHIM6', 'WESP', 'ROHC', 'ALL'.
* port (string, optional): The port (Can be prot range).
* openForAll (boolean): True if it is open for the entrie internet, flase if it isn't.
* scope (Array[ScopeElementViewModel], optional): The service scope, If the service is "close" then the scope isn't needed.
  * type (string): Can be one of the next - ['CIDR', 'DNS', 'IPList', 'MagicIP', 'AWS'],
  * data (object): For CIDR - "cidr":'IP', For IP-List - "id":"IP-LIST ID","name":"IP-LIST NAME"}
* inbound (boolean): If true the rule will be add to the inbound, if false it will be add to outbound.
* icmpType (string, optional): In case of ICMP - 'EchoReply', 'DestinationUnreachable', 'SourceQuench', 'Redirect', 'AlternateHostAddress', 'Echo', 'RouterAdvertisement', 'RouterSelection', 'TimeExceeded', 'ParameterProblem', 'Timestamp', 'TimestampReply', 'InformationRequest', 'InformationReply', 'AddressMaskRequest', 'AddressMaskReply', 'Traceroute', 'DatagramConversionError', 'MobileHostRedirect', 'IPv6WhereAreYou', 'IPv6IAmHere', 'MobileRegistrationRequest', 'MobileRegistrationReply', 'DomainNameRequest', 'DomainNameReply', 'SKIP', 'Photuris', 'All'


<h3><a name="aws-security-groups-overwrite-service">Overwrite service</a></h3>

Update an existing service, the service will be fully overwrite.

URL: https://api.dome9.com/cloudsecuritygroup/{groupid}/services <br \>
METHOD: PUT

note: The groupid in the url can be eithe the internal id or the external id.

BODY:
```json
{
  "name": "string",
  "description": "string",
  "protocolType": "string",
  "port": "string",
  "openForAll": boolean,
  "scope": [
    {
      "type": "string",
      "data": object
    }
  ],
  "inbound": boolean,
  "icmpType": "string"
}
```

####Request parameters

* name (string): The service name.
* description (string, optional): The service description.
* protocolType (string): Can be one od the next protocols - 'HOPOPT', 'ICMP', 'IGMP', 'GGP', 'IPV4', 'ST', 'TCP', 'CBT', 'EGP', 'IGP', 'BBN_RCC_MON', 'NVP2', 'PUP', 'ARGUS', 'EMCON', 'XNET', 'CHAOS', 'UDP', 'MUX', 'DCN_MEAS', 'HMP', 'PRM', 'XNS_IDP', 'TRUNK1', 'TRUNK2', 'LEAF1', 'LEAF2', 'RDP', 'IRTP', 'ISO_TP4', 'NETBLT', 'MFE_NSP', 'MERIT_INP', 'DCCP', 'ThreePC', 'IDPR', 'XTP', 'DDP', 'IDPR_CMTP', 'TPplusplus', 'IL', 'IPV6', 'SDRP', 'IPV6_ROUTE', 'IPV6_FRAG', 'IDRP', 'RSVP', 'GRE', 'DSR', 'BNA', 'ESP', 'AH', 'I_NLSP', 'SWIPE', 'NARP', 'MOBILE', 'TLSP', 'SKIP', 'IPV6_ICMP', 'IPV6_NONXT', 'IPV6_OPTS', 'CFTP', 'SAT_EXPAK', 'KRYPTOLAN', 'RVD', 'IPPC', 'SAT_MON', 'VISA', 'IPCV', 'CPNX', 'CPHB', 'WSN', 'PVP', 'BR_SAT_MON', 'SUN_ND', 'WB_MON', 'WB_EXPAK', 'ISO_IP', 'VMTP', 'SECURE_VMTP', 'VINES', 'TTP', 'NSFNET_IGP', 'DGP', 'TCF', 'EIGRP', 'OSPFIGP', 'SPRITE_RPC', 'LARP', 'MTP', 'AX25', 'IPIP', 'MICP', 'SCC_SP', 'ETHERIP', 'ENCAP', 'GMTP', 'IFMP', 'PNNI', 'PIM', 'ARIS', 'SCPS', 'QNX', 'AN', 'IPCOMP', 'SNP', 'COMPAQ_PEER', 'IPX_IN_IP', 'VRRP', 'PGM', 'L2TP', 'DDX', 'IATP', 'STP', 'SRP', 'UTI', 'SMP', 'SM', 'PTP', 'ISIS', 'FIRE', 'CRTP', 'CRUDP', 'SSCOPMCE', 'IPLT', 'SPS', 'PIPE', 'SCTP', 'FC', 'RSVP_E2E_IGNORE', 'MOBILITY_HEADER', 'UDPLITE', 'MPLS_IN_IP', 'MANET', 'HIP', 'SHIM6', 'WESP', 'ROHC', 'ALL'.
* port (string, optional): The port (Can be prot range).
* openForAll (boolean): True if it is open for the entrie internet, flase if it isn't.
* scope (Array[ScopeElementViewModel], optional): The service scope, If the service is "close" then the scope isn't needed.
  * type (string): Can be one of the next - ['CIDR', 'DNS', 'IPList', 'MagicIP', 'AWS'],
  * data (object): For CIDR - "cidr":'IP', For IP-List - "id":"IP-LIST ID","name":"IP-LIST NAME"}
* inbound (boolean): If true the rule will be add to the inbound, if false it will be add to outbound.
* icmpType (string, optional): In case of ICMP - 'EchoReply', 'DestinationUnreachable', 'SourceQuench', 'Redirect', 'AlternateHostAddress', 'Echo', 'RouterAdvertisement', 'RouterSelection', 'TimeExceeded', 'ParameterProblem', 'Timestamp', 'TimestampReply', 'InformationRequest', 'InformationReply', 'AddressMaskRequest', 'AddressMaskReply', 'Traceroute', 'DatagramConversionError', 'MobileHostRedirect', 'IPv6WhereAreYou', 'IPv6IAmHere', 'MobileRegistrationRequest', 'MobileRegistrationReply', 'DomainNameRequest', 'DomainNameReply', 'SKIP', 'Photuris', 'All'

<h3><a name="aws-security-groups-delete-service">Delete service</a></h3>

Delete an existing service.

URL: https://api.dome9.com/cloudsecuritygroup/{groupid}/services/{serviceid}?inbound={boolean} <br \>
METHOD: DELETE

* serviceid: compose from the port and protocol type with the next structure "{port}-{protocol type}",for example in ssh case it will be "6-22".
* groupid: The groupid in the url can be eithe the internal id or the external id.
* inbound: If true it will delete in the inbound and if false in the oubound.

<h3><a name="aws-security-groups-delete-security-groups">Delete Security Groups</a></h3>

Delete an existing security group.

URL: https://api.dome9.com/cloudsecuritygroup/{groupid} <br \>
METHOD: DELETE

* groupid: The groupid in the url can be eithe the internal id or the external id.



##<a name="aws-accounts">AWS Accounts</a>

###Add AWS Account.

Add a new AWS account to your Dome9 account.

URL: https://api.dome9.com/CloudAccounts <br \>
METHOD: POST
BODY:
```json
{
  "name": "string",
  "credentials": {
    "arn": "string" /*required*/, 
    "secret": "string" /*required*/,
    "type": "RoleBased" /*required*/,
    "isReadOnly": boolean
  },
  "fullProtection": true
}
```

####Request parameters

* name (string, optional): The account name on Dome9.
* credentials (object, required): AWS account credentials.
  * arn (string, required): The predefine AWS role for Dome9.
  * secret (string, required): The role External ID.
  * type (string, required): 'RoleBased'.
  * isReadOnly (boolean, optional): The attached policy type.
* fullProtection (boolean, optional): True if to import the security groups in full protection or false in read only mode.

###Update AWS Account.

Update an existing attached AWS account.

URL: https://api.dome9.com/CloudAccounts/{id} <br \>
METHOD: PATCH
id: The Dome9 cloud account ID
BODY:
```json
{
  "name": "string",
  "credentials": {
    "arn": "string" , 
    "secret": "string" ,
    "type": "RoleBased" ,
    "isReadOnly": boolean
  },
  "fullProtection": boolean,
  "netSec": {
      "regions": [
        {
          "region": "string",
          "hidden": boolean,
          "newGroupBehavior": boolean
        }
      ]
    }
}
```

####Request parameters

* name (string, optional): The account name on Dome9.
* credentials (object, required): AWS account credentials.
  * arn (string, required): The predefine AWS role for Dome9.
  * secret (string, required): The role External ID.
  * type (string, required): 'RoleBased'.
  * isReadOnly (boolean, optional): The attached policy type.
* fullProtection (boolean, optional): True if to import the security groups in full protection or false in read only mode.
* regions: The region data, it possible to insert only one region on each request.
  * region (string, optional): Can be one of the next options - 'us_east_1', 'us_west_1', 'eu_west_1', 'ap_southeast_1', 'ap_northeast_1', 'us_west_2', 'sa_east_1', 'az_1_region_a_geo_1', 'az_2_region_a_geo_1', 'az_3_region_a_geo_1', 'ap_southeast_2', 'mellanox_region', 'us_gov_west_1', 'eu_central_1', 'ap_northeast_2'
  * hidden (boolean, optional): True if the security groups in region will be displayed or false to hide them. 
  * newGroupBehavior (string, optional): Can be one of the next options - 'ReadOnly', 'FullManage', 'Reset'.

###Delete AWS Account

Delete an existing AWS Account.

URL: https://api.dome9.com/CloudAccounts/{cloudAccountId} <br \>
METHOD: DELETE

* cloudAccountId: The Dome9 cloudAccountId.

##<a name="ip-lists">IP Lists</a>

###GET 

The get request pull the entire IP Lists which attached to the Dome9 account.
ID: If the request is made without the IP List id then the entire IP Lists will return.

URL: https://api.dome9.com/IpList/{id} <br \>
METHOD: GET

####Response
```json
[
  {
    "id": 0,
    "name": "string",
    "description": "string",
    "items": [
      {
        "ip": "string",
        "comment": "string"
      }
    ]
  }
]
```

* id (integer): The IP List Id.
* name (string): The IP List name.
* description (string): The IP List description.
* items (Array[IPDescriptor]): An array with the Ips.
  * ip (string): IP address.
  * comment (string): A comment on the ip if exist.

###Create IP List
Create a new IP List.

URL: https://api.dome9.com/IpList <br \>
METHOD: POST
BODY:
```json
{
  "name": "string", /* required */
  "description": "string",
  "items": [
    {
      "ip": "string", /* required */
      "comment": "string"
    }
  ]
}
```

####Request parameters

* name (string): The IP List name.
* description (string): The IP List description.
* items (Array[IPDescriptor]): An array with the Ips.
  * ip (string): IP address.
  * comment (string): A comment on the ip if exist.


###Update IP List
Update an existing IP LIst.
The Updaate is relevant for the data and the description.
It will overwrite the existing IP List.

URL: https://api.dome9.com/IpList/{id} <br \>
METHOD: PUT

BODY:
```json
{
  "name": "string",
  "description": "string",
  "items": [
    {
      "ip": "string",
      "comment": "string"
    }
  ]
}
```

####Request parameters
* id (in the url): is the IP List ID
* name (string): The IP List name.
* description (string): The IP List description.
* items (Array[IPDescriptor]): An array with the Ips.
  * ip (string): IP address.
  * comment (string): A comment on the ip if exist.
 
###Delete IP List

Delete an existing IP List.

URL: https://api.dome9.com/IpList/{id} <br \>
METHOD: DELETE

* id: The IP List Id.
  
