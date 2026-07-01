# neptunesoftware-dxp-mcp-goods-receipt
Goods Receipt MCP Template

## Table of Contents
- [Overview](#overview)
- [Prerequisites](#prerequisites)
  - [Neptune DXP SAP Integration Hub Prerequisites](#neptune-dxp-sap-integration-hub-prerequisites)
  - [Neptune DXP Open Edition Prerequisites](#neptune-dxp-open-edition-prerequisites)
  - [Neptune DXP Version Compatibility](#neptune-dxp-version-compatibility)
    - [Neptune DXP SAP Edition Version](#neptune-dxp-sap-edition-version)
    - [Neptune DXP Open Edition Version](#neptune-dxp-open-edition-version)
  - [Recommended Naming Conventions & Namespaces](#recommended-naming-conventions--namespaces)
- [Neptune DXP SAP Edition Setup](#neptune-dxp-sap-edition-setup)
  - [Step 1. Import the Included Transport File Into Your SAP System](#neptune-dxp-sap-edition-setup)
  - [Step 2. Access the Imported Custom Data Provider Class](#neptune-dxp-sap-edition-setup)
- [Neptune DXP Open Edition Setup](#neptune-dxp-open-edition-setup)
  - [Step 3. Connecting the included MCP Server Connection in Open Edition to Your Configured Remote System Connection](#step-3-connecting-the-included-api-in-open-edition-to-the-newly-created-api-factory-api-in-sap-edition)

## Overview

This bundle demonstrates a **SAP Goods Receipt** workflow, providing a simple reference implementation for interacting via an AI Agent with production orders and posting goods receipts to the SAP backend.

If you're interested in using this marketplace template with AI-powered editors and assistants, for example, Claude Code, Claude Desktop, Cursor, and Windsurf, manage your design-time artifacts directly through natural-language instructions... 
This documentation [MCP Server](https://docs.neptune-software.com/neptune-dxp-open-edition/24.15/mcp-server/overview.html) explains how to connect a supported MCP client, how authorization works for end users, which artifacts you can manage through MCP, and how to resolve common connection issues. Instructions are intended for developers, designers, and administrators who use Neptune DXP - Open Edition.

### Features

The bundle supports the following use cases:

- 📋 **View Production Orders**
  - Retrieve and display production orders from SAP.

- ❓ **Answer Questions About Production Orders**
  - Provide information about production order details, status, materials, and quantities.

- ✍️ **Enter Goods Receipt Quantities**
  - Guide users through entering the quantities received for a production order.

- ✅ **Post Goods Receipts**
  - Submit the goods receipt to SAP once the quantities have been confirmed.

## Prerequisites
Before implementing this integration scenario, ensure that the following prerequisites are met.

### Neptune DXP SAP Integration Hub Prerequisites:
- Neptune DXP SAP Integration Hub - Minimum version 1.1.0
- A valid Neptune Subscription License is active. 
- The SAP user must have the required SAP authorizations to access, create & activate custom ABAP artifacts, including data provider classes (_**'ZCL'**_) and using the transaction _**'SE24'**_.
- The SAP user must be authorized to read and write data in the SAP backend system through _Function Modules_ and _BAPIs_ that are consumed by the custom ABAP logic.
- The SAP user must have the required SAP authorizations to import Transport Order files to their SAP system.
- Neptune DXP – SAP Integration Hub is installed and configured in your SAP system -> You can read more on how to install [Neptune DXP - SAP Integration Hub](https://docs.neptune-software.com/neptune-sap-edition/24.15/cockpit-overview/sap-integration-manual-installation.html) here. 

### Neptune DXP Open Edition Prerequisites:
- Neptune DXP Open Edition - Minimum version 24.15.0
- A valid Neptune Subscription License is active.
- A connection to your SAP system has been configured using the [Remote Systems](https://docs.neptune-software.com/neptune-dxp-open-edition/24.15/cockpit-overview/security-remote-systems.html) tool in Neptune DXP Open Edition.
- In Neptune DXP Open Edition, the user must have [Role](https://docs.neptune-software.com/neptune-dxp-open-edition/24.15/cockpit-overview/security-role.html) based access to create and maintain artifacts, including _'MCP server connections'_ via the [Hub MCP Designer](https://docs.neptune-software.com/neptune-dxp-open-edition/24.15/cockpit-overview/sap-integration-hub-mcp-designer.html) and _agents_ via the [Agents](https://docs.neptune-software.com/neptune-dxp-open-edition/24.15/cockpit-overview/ai-agents.html).
- The user must have [role](https://docs.neptune-software.com/neptune-dxp-open-edition/24/cockpit-overview/security-role.html) based access to create and maintain [Proxy Authentication](https://docs.neptune-software.com/neptune-dxp-open-edition/24/cockpit-overview/security-proxy-auth.html) artifacts that need to be added to a remote system connection in Neptune DXP Open Edition.


## Neptune DXP Version Compatibility
While the Neptune DXP - SAP Integration Hub and Open Edition cater to different user environments and have unique requirements, leveraging this bundle with an end-to-end solution across both versions in mind, requires understanding their compatibility.

Users can only import the MCP Goods Receipt bundle into DXP version 24.15.0 of Neptune DXP Open Edition

### Neptune DXP SAP Integration Hub Version
Recommended Version: _**Neptune DXP SAP Integration Hub 1.1.0**_
Released: Q2/2026

### Neptune DXP Open Edition Version
Recommended Version: _**Neptune DXP - Open Edition 24.15.0**_
Released: Q2/2026

## Recommended Naming Conventions & Namespaces
To ensure a streamlined and consistent import process for the provided source files that implement the exposure of ABAP-based business logic in the SAP backend system, it is recommended to retain the naming conventions and namespaces as defined in the included artifacts of the Transport Order file.

The included transport order file for SAP includes the implementation of an ABAP Data Provider Class, which serves as the central integration component for the MCP Server connection (this MCP Server connection is also included in the SAP package & created via the Hub MCP Designer in Neptune DXP Open Edition).

## Manual Steps Guide for Neptune DXP Open Edition + SAP (with SAP Integration HUB installed)
This guide provides a step-by-step walkthrough for manually configuring and unlocking the full capabilities of this Marketplace template with Neptune DXP Open Edition and SAP (with SAP Integration Hub installed).

To complete the setup successfully, follow each step in order. During this process, you will:

* Verify that an MCP remote system connection has been configured.
* Import the included SAP transport request (.zip file).
* Navigate to the **Hub MCP Designer** to explore the Marketplace template's MCP server connection.
* Open the **Agent** tool to explore the included AI Agent and its capabilities.


### Step 0. Configure a remote system connection in Neptune DXP Open Edition
If you have already a remote system (Type _**Model Context Protocol**_) connection configured in your Neptune DXP Open Edition instance, you can skip this step.

The very first step you need to take... is to condfigure a remote system connection in your Neptune DXP Open Edition via the [Remote Systems](https://docs.neptune-software.com/neptune-dxp-open-edition/24.15/cockpit-overview/security-remote-systems.html) tool.

This remote connection **MUST** be Type "_Model Context Protocol_":
<img width="1193" height="384" alt="image" src="https://github.com/user-attachments/assets/40a08ef2-4bd6-4ee0-9a02-f111eacd9354" />

_**NOTE:**_ Ensure that this newly configured remote system connection is targeting the SAP system that has SAP Integration Hub installed and it's the same system where you'll import the included transport file. _**(details provided in Step. 1)**_

### Step 1. Import the included transport file to your SAP system

Begin by dowloading the included transport file "_**transport_K_R_996120.zip**_" located at the root of the repository.
In this .zip file, you'll find a "K996120.NAI" and a "R996120.NAI" file to be imported to your SAP system.
These will contain the custom ABAP Data Provider Class _(TCode SE24)_ and an MCP server connection _(will be visible in the Hub MCP Designer in your Neptune DXP Open Edition instance)_

### Step 2. Access the Hub MCP Designer in your Neptune DXP Open Edition instance

After successfully importing the included transport order .zip file to your SAP system... Navigate to your Neptune DXP Open Edition cockpit and access the _**Hub MCP Designer**_ tool.
<img width="1854" height="580" alt="image" src="https://github.com/user-attachments/assets/7b95254b-16c8-49b2-bcdc-f4f20cf3181a" />

In this tool, you can create & maintain your own MCP server connections, configuring the tools that you want the AI agent to use - to send & get data from your SAP system.
<img width="1832" height="825" alt="image" src="https://github.com/user-attachments/assets/ae20fcd9-a2f5-495b-adfb-583ce71fdb57" />

Ensure that you enable / disable the tools available from this marketplace template to be used via an AI Agent.
<img width="1823" height="888" alt="image" src="https://github.com/user-attachments/assets/ee90d3cd-acc2-4e73-95cc-0e2280e5441f" />

### Step 3. Navigate to the Agent tool in your Neptune DXP Open Edition instance
With the MCP server in place, the next step is to validate the included AI agent that will leverage the SAP business logic exposed through your MCP tools.
<img width="1264" height="519" alt="image" src="https://github.com/user-attachments/assets/0adbc4ff-4e07-40da-bef2-33fa9781c82e" />

**_NOTE: Ensure to assign a Model to this AI Agent, you will need to manully configure this step in order to fully leverage the AI Agent capabilities_**
<img width="1834" height="589" alt="image" src="https://github.com/user-attachments/assets/76f7ed9a-11ba-417c-bec1-66195a2ad3e1" />

To create your own Reference AI Model, you read more in our public documentation about [Models](https://docs.neptune-software.com/neptune-dxp-open-edition/24.15/cockpit-overview/ai-models.html) 
<img width="1218" height="355" alt="image" src="https://github.com/user-attachments/assets/99c01935-9999-441a-ba0f-88772679ca75" />

Within the agent configuration, you can define instructions that guide how the agent should interact with users and when it should invoke MCP tools. These instructions help the agent determine which information needs to be collected from the user, how to pass that information to SAP, and how to present the results returned from SAP.
<img width="1813" height="1516" alt="image" src="https://github.com/user-attachments/assets/bdcd9917-79ef-4939-9cb3-a19a122b2278" />

