# Awesome AutomationFX

A curated list of AutomationFX resources for Developers, inspired by [awesome-ciscospark](https://github.com/CiscoDevNet/awesome-ciscospark) and [awesome-python](https://github.com/vinta/awesome-python).

### Contents

- [AutomationFX](#automationfx)
- [REST API](#rest-api)
- [SDK](#sdk)
- [Authentication](#authentication)
- [CUCM Support](#cucm-support)
- [Cloud Integration](#cloud-integration)
    - [CloudFX](#cloudfx)
- CUCM API's Supported
    - [AXL](#axl)
    - CTI
    - RISPort

DISCLAIMER: [UnifiedFX](http://www.unifiedfx.com) does not make any commitments about the resources listed in this document, nor the accuracy of the third party resources and any content accessible via those links.

## AutomationFX

*AutomationFX is a integration platform from [UnifiedFX](http://www.unifiedfx.com) that exposes Cisco Unified Communication Managers (CUCM) complex and varied interfaces via a simple unified REST API.*
*Note: Currently AutomationFX software is only availble under NDA, however once AutomaitonFX is officially released it will be available for general download. Please contact [UnifiedFX Sales](mailto:sales@unifiedfx.com) for further information and request access to the software.*

## REST API

*The REST API exposed by AutomationFX provides access to multiple CUCM resources. Sometimes this is effectively a one-two-one mapping to an existing API (i.e. AXL). Sometimes this is a combination of multiple datasets to provide a more cohesive view.*

* AutomationFX API Documentation
    * All REST API operations are documented using [Swagger](https://swagger.io)
    * Preview the API using Swagger UI Online [Live AutomationFX Demo](http://petstore.swagger.io/?url=https://raw.githubusercontent.com/unifiedfx/awesome-automationfx/master/automationfx-swagger.json)
    * There is a built-in implimentation of Swagger UI that provides live testing against CUCM for all operations within AutomationFX. This is similar to [Cisco Spark SDK](https://developer.ciscospark.com/getting-started.html)
    * [AutomationFX Swagger Specification](https://github.com/unifiedfx/awesome-automationfx/blob/master/automationfx-swagger.json)

*Currently the following CUCM API's are exposed via AutomationFX:*


* [AXL](https://developer.cisco.com/site/axl) - Cisco Administrive XML
* [CTI](https://developer.cisco.com/site/jtapi) - Computer Telephony Integration (JTAPI)
* [RISPort](https://developer.cisco.com/site/sxml/discover/overview/risport/) - Real-Time Information Port

## SDK
Software Development Kits (SDK) make it simple to get up and running in a familiar environment. The first SDK for AutomationFX is available in [Python](https://www.python.org/about/gettingstarted/)

* [Python](https://github.com/unifiedfx/automationfx-python) - Python SDK for AutomationFX


## Authentication

*AutomationFX currently supports three authentication mechanisms:*

* Basic (Validates credentials against an Application or End User on CUCM)
    * The User must have one of the following permissions:
        * Standard CCM Phone Administration
        * Standard CCM Admin
* Cookie
    * This is ideal for leveraging AutomationFX to create a custom web application letting AutomationFX take care of the authentication as well as the facilities of the REST API
    * Use the built-in login page (http://127.0.0.1:8181/login)
    * POST a JSON object i.e. {'userId':'guest','password':'ufx12345'} to the above URL and obtain the cookie
* APIKey (Can be added as a Header or query string parameter)
    * i.e. https://api.unifiedfx.com?apikey=XXX
    * Currently the API Key is only enabled/provided on request

## CUCM Support

*AutomationFX support all versions of CUCM starting from 8.0 (including CUCM 12.0)*

## Cloud Integration

*By design AutomationFX is not just about simplifying integration with CUCM, but providing integration with cloud services in the exact same way as [Cisco Spark](https://www.ciscospark.com). This enables existing CUCM systems to leverage the trend towards modern cloud and devops based application enablement of Unified Communications.*

*AutomationFX can be deployed to a DMZ location as long as the appropriate services are open. However in order to simplify testing and development AutomationFX has a build in 'Cloud Relay' ([CloudFX](#cloudfx)) that maintains an out-bound connection to a secure relay end-point.*

### CloudFX
*CloudFX is similar to facilities like [ngrok](https://ngrok.com), but secured to only allow specific well-formatted requests and DDOS control. The CloudFX relay endpoint (https://api.unifiedfx.com) uses an APIKey to authenticate and route the request to the corresponding on-premise AutomationFX instance. This enabled a multitude of integration options using services like [Zapier](https://zapier.com), [built.io](https://www.built.io), [hook.io](https://hook.io), [IFTTT](https://ifttt.com)*

*The following video is a demo of integrating Cisco Spark and CUCM. In this example Zapier is used to integrate with AutomationFX, however any of the above cloud services could be used:*

* [Spark and CUCM integration via AutomationFX and Zapier](https://youtu.be/K0H5xtfyrf4)

[![IMAGE ALT TEXT](http://img.youtube.com/vi/K0H5xtfyrf4/0.jpg)](https://www.youtube.com/watch?v=K0H5xtfyrf4 "Spark and CUCM integration via AutomationFX and Zapier")

## AXL

*AutomationFX effectively translates the native CUCM AXL SOAP Actions to RESTful Resources. The REST API accepts and can return XML or JSON resource models. JSON support is partucularly useful as it provides the ability to embedd the AutomationFX REST API directly inside a browser applicaiton. For example this would allow the creation of a custom provisioning interface as an alterantive to CCMAdmin. The followng is an example of the mapping between AXL SOAP Actions for CRUD operations on a phone in CUCM and the corresponding REST Operation:*

* ListPhone => GET /AutomationFX/api/axl/phone
* AddPhone => POST /AutomationFX/api/axl/phone
* GetPhone => GET /AutomationFX/api/axl/phone/SEP123456789012
* UpdatePhone => PUT /AutomationFX/api/axl/phone/SEP123456789012
* RemovePhone => DELETE /AutomationFX/api/axl/phone/SEP123456789012