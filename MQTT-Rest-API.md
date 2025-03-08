# MQTT API Documentation

**Table of Contents**

* [Broker Connection Details](#broker-connection-details)
* [General Notes](#general-notes)
1.  [Project Actions](#1-project-actions)
    * [1.1. Get Project](#11-get-project)
    * [1.2. Edit Project](#12-edit-project)
    * [1.3. Get All Areas](#13-get-all-areas)
    * [1.4. Get All Zones](#14-get-all-zones)
    * [1.5. Get All Nodes](#15-get-all-nodes)
    * [1.6. Get All Gateways](#16-get-all-gateways)
2.  [Area Actions](#2-area-actions)
    * [2.1. Get Area](#21-get-area)
    * [2.2. Create Area](#22-create-area)
    * [2.3. Edit Area](#23-edit-area)
    * [2.4. Delete Area](#24-delete-area)
    * [2.5. Get All Zones](#25-get-all-zones)
    * [2.6. Get All Nodes](#26-get-all-nodes)
    * [2.7. Get All Gateways](#27-get-all-gateways)
3.  [Zone Actions](#3-zone-actions)
    * [3.1. Get Zone](#31-get-zone)
    * [3.2. Create Zone](#32-create-zone)
    * [3.3. Edit Zone](#33-edit-zone)  
    * [3.4. Delete Zone](#34-delete-zone)
    * [3.5. Get All Nodes](#35-get-all-nodes)
    * [3.6. Get Zone Added Gateways](#36-get-zone-added-gateways) 
4.  [Node Actions](#4-node-actions)
    * [4.1. Get Node](#41-get-node)
5.  [Gateway Actions](#5-gateway-actions)
    * [5.1. Get Gateway](#51-get-gateway)
6. [Zone Operations](#6-zone-operations)
    * [6.1 Get CCT Zone Status](#61-get-cct-zone-status)
    * [6.2 Get Dimmer Zone Status](#62-get-dimmer-zone-status)
    * [6.3 Get Presence Sensor Zone Status](#63-get-presence-sensor-zone-status)
    * [6.4 Control CCT Zone](#64-control-cct-zone)
    * [6.5 Control Dimmer Zone](#65-control-dimmer-zone)
    * [6.6 Get Entery Exit Sensor Zone Status](#66-get-entery-exit-sensor-zone-status)
    * [6.7 Get Lux Sensor Zone Status](#67-get-lux-sensor-zone-status)
    * [6.8 Get Temperature Humidity Sensor Zone Status](#68-get-temperature-humidity-sensor-zone-status)
7. [Node Operations](#7-node-operations)
    * [7.1 Get CCT Node Status](#71-get-cct-node-status)
    * [7.2 Get Dimmer Node Status](#72-get-dimmer-node-status)
    * [7.3 Control CCT Node](#73-control-cct-node)
    * [7.4 Control Dimmer Node](#74-control-dimmer-node)
    * [7.5 Get Presence Senser Node Status](#75-get-presence-sensor-node-status)
    * [7.6 Get Entery Exit Sensor Node Status](#76-get-entery-exit-sensor-node-status)
    * [7.7 Get Lux Sensor Node Status](#77-get-lux-sensor-node-status)
    * [7.8 Get Temperature Humidity Sensor Node Status](#78-get-temperature-humidity-sensor-node-status)
    * [7.9 Get Parking Sensor Node Status](#79-get-parking-sensor-node-status) 
8. [Gateway Operations](#8-gateway-operations)
    * [8.1 Get Gateway Status](#81-get-gateway-status)
9. [Live Events](#9-live-events])
    * [9.1 Edit Project](#91-edit-project)
    * [9.2 Delete Project](#92-delete-project)
    * [9.3 Create Area](#93-create-area)
    * [9.4 Edit Area](#94-edit-area)
    * [9.5 Delete Area](#95-delete-area)
    * [9.6 Create Zone](#96-create-zone)
    * [9.7 Edit Zone](#97-edit-zone)
    * [9.8 Delete Zone](#98-delete-zone)
    * [9.9 Geteway Status](#99-gateway-status)
    * [9.10 Node Status](#910-node-status) 
11. [Error Message](#10-error-messages)

## Broker Connection Details

* **URL:** `mqtt://192.168.0.111:1883`
* **Username:** `admin`
* **Password:** `admin@123`

## General Notes

* All payloads are in JSON format.
* All topics follow a hierarchical structure: `LYT/<project_uuid>/<entity>/<action_type>`
* Response topics typically append `/E` to the entity part of the request topic.
* limit and offset perameter is optional. by default limit set 50.

## 1. Project Actions

### 1.1. Get Project

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/PROJECT/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "get"
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "get").

* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/PROJECT/E/ACTION`
* **Response Payload:**

    ```json
    {
      "message": "success",
      "version": "v1.0",
      "action": "get",
      "data": {
        "project_uuid": "7346d2b3-ee78-4907-b6cb-c936b8aed1b1",
        "name": "Demo",
        "project_type": "Healthcare"
      }
    }
    ```

    * `message`: Status of the request (e.g., "success").
    * `version`: API version.
    * `action`: Action to perform (e.g., "get").
    * `data`: Project details.
        * `project_uuid`: Unique identifier of the project.
        * `name`: Name of the project.
        * `project_type`: Type of the project.
     
### 1.2. Edit Project

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/PROJECT/ACTION`
* **Request Payload:**

   ```json
   {
     "version": "v1.0",
     "action": "edit",
     "data": {
       "name": "demo",
       "project_type": "Workspace"
     }
   }
   ```

   * `version`: API version.
   * `action`: Action performed.
   * `data`:
       * `name`:The name of the project.
       * `project_type`:The type of the project, which must be one of the supported types. - `Healthcare` - `Workspace` - `Education`
    

* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/PROJECT/E/ACTION`
* **Response Payload:**

   ```json
   {
     "action": "edit",
     "message": "success",
     "version": "v1.0",
     "data": {
         "project_uuid": "7346d2b3-ee78-4907-b6cb-c936b8aed1b1",
         "name": "demo",
         "project_type": "Workspace"
      }
   }
   ```
   * `version`: API version.
   * `action`: Action performed.
   * `message`: Status of the request.
   * `data`:
      * `project_uuid`: The unique identifier of the project.
      * `name`: The updated name of the project.
      * `project_type`: The updated project type, ensuring it matches the supported types.

### 1.3. Get All Areas

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/PROJECT/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "get-all-areas",
      "limit": 10,
      "offset": 0
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "get-all-areas").
    * `limit`: (Optional) Maximum number of areas to return. Default: 50.
    * `offset`: (Optional) Starting position for the results. Default: 0.

* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/PROJECT/E/ACTION`
* **Response Payload:**

    ```json
    {
      "message": "success",
      "version": "v1.0",
      "action": "get-all-areas",
      "data": [
        {
          "area_uuid": "f1677ff1-0138-47a0-b202-5de5e83827a0",
          "name": "A514 office",
          "project_uuid": "7346d2b3-ee78-4907-b6cb-c936b8aed1b1"
        },
        {
          "area_uuid": "cc8b1728-7d43-433f-87ba-bd14dbb1953e",
          "name": "Demo ......",
          "project_uuid": "7346d2b3-ee78-4907-b6cb-c936b8aed1b1"
        },
        {
          "area_uuid": "65635a43-b07f-466b-91de-cb166a3df48f",
          "name": "Demo",
          "project_uuid": "7346d2b3-ee78-4907-b6cb-c936b8aed1b1"
        },
        {
          "area_uuid": "49f9dd1e-057c-4718-ab5b-fbe9242f2b25",
          "name": "Demo 1",
          "project_uuid": "7346d2b3-ee78-4907-b6cb-c936b8aed1b1"
        },
        {
          "area_uuid": "8625323f-d800-44f8-845e-595cfa35cad1",
          "name": "Demo 2",
          "project_uuid": "7346d2b3-ee78-4907-b6cb-c936b8aed1b1"
        }
      ]
    }
    ```

    * `message`: Status of the request.
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Array of area objects.
        * `area_uuid`: Unique identifier of the area.
        * `name`: Name of the area.
        * `project_uuid`: Unique identifier of the project.

### 1.4. Get All Zones

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/PROJECT/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "get-all-zones",
      "limit": 10,
      "offset": 0
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "get-all-zones").
    * `limit`: (Optional) Maximum number of zones to return. Default: 50.
    * `offset`: (Optional) Starting position for the results. Default: 0.

* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/PROJECT/E/ACTION`
* **Response Payload:**

    ```json
    {
      "message": "success",
      "version": "v1.0",
      "action": "get-all-zones",
      "data": [
        {
          "zone_address": 50646,
          "name": "First zone",
          "area_uuid": "f1677ff1-0138-47a0-b202-5de5e83827a0",
          "area_name": "A514 office",
          "zone_uuid": "63ab9c4b-08f3-437e-a448-0eab7c9e1420"
        }
      ]
    }
    ```

    * `message`: Status of the request.
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Array of zone objects.
        * `zone_address`: Address of the zone.
        * `name`: Name of the zone.
        * `area_uuid`: Unique identifier of the area.
        * `area_name`: Name of the area.
        * `zone_uuid`: Unique identifier of the zone.

### 1.5. Get All Nodes

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/PROJECT/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "get-all-nodes",
      "limit": 10,
      "offset": 0
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "get-all-nodes").
    * `limit`: (Optional) Maximum number of nodes to return. Default: 50.
    * `offset`: (Optional) Starting position for the results. Default: 0.

* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/PROJECT/E/ACTION`
* **Response Payload:**

    ```json
    {
        "message": "success",
        "version": "v1.0",
        "action": "get-all-nodes",
        "data": [
            {
                "node_uuid": "bbcc84f7-0316-4ec6-0000-000000000000",
                "name": "LYTIVA_164EC6",
                "pid": "1015",
                "vid": "0263",
                "unicast_address": 5743,
                "zone_uuid": "63ab9c4b-08f3-437e-a448-0eab7c9e1420",
                "zone_name": "First zone",
                "zone_address": 50646,
                "model_id": "1303",
                "device_type": "ctl"
            },
            {
                "node_uuid": "bbcc84f7-0316-3716-0000-000000000000",
                "name": "LYTIVA_163716",
                "pid": "1015",
                "vid": "0263",
                "unicast_address": 1345,
                "zone_uuid": "06168eeb-7ca5-49e7-a769-7073347af48f",
                "zone_name": "Second Zone",
                "zone_address": 49536,
                "model_id": "1303",
                "device_type": "ctl"
            }
        ]
    }
    ```

    * `message`: Status of the request.
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Array of node objects.
        * `node_uuid`: Unique identifier for the node
        * `name`: Name of the node.
        * `zone_address`: Address of the zone.
        * `pid`: Product id
        * `vid`: Version id
        * `unicast_address`: Node unicast address
        * `zone_uuid`: Unique identifier of the zone.
        * `zone_name`: Zone name
        * `zone_address`: Zone address
        * `model_id`: Model identifier
        * `device_type`: Type of device
        * 

### 1.6. Get All Gateways

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/PROJECT/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "get-all-gateways",
      "limit": 10,
      "offset": 0
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "get-all-nodes").
    * `limit`: (Optional) Maximum number of nodes to return. Default: 50.
    * `offset`: (Optional) Starting position for the results. Default: 0.

* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/PROJECT/E/ACTION`
* **Response Payload:**

    ```json
    {
       "message": "success",
       "version": "v1.0",
       "action": "get-all-gateways",
       "data": [
           {
               "gateway_uuid": "aaaa84f7-036e-8d2e-0000-000000000000",
               "name": "AERIVA_6E8D2E",
               "pid": "1041",
               "vid": "0111",
               "area_uuid": "f1677ff1-0138-47a0-b202-5de5e83827a0",
               "area_name": "A514 office",
               "unicast_address": 249
           }
       ]
   }
   ```

    * `message`: Status of the request.
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Array of gateway objects.
        * `gateway_uuid`: Unique identifier for the gateway
        * `name`: Name of the gateway.
        * `pid`: Product id
        * `vid`: Version id
        * `unicast_address`: Gateway unicast address
        * `area_uuid`: Unique identifier of the area.
        * `area_name`: Area name
     

## 2. Area Actions

### 2.1. Get Area

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "get",
      "data": {
          "area_uuid": "f1677ff1-0138-47a0-b202-5de5e83827a0"
       }
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "get").
    * `data`: Area details.
        * `area_uuid`: Unique identifier of the area.
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/E/ACTION`
* **Response Payload:**

    ```json
    {
       "message":"success",
       "version":"v1.0",
       "action":"get",
       "data":{
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0",
          "name":"A514 office",
          "project_uuid":"7346d2b3-ee78-4907-b6cb-c936b8aed1b1"
       }
    }
    ```

    * `message`: Status of the request (e.g., "success").
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Area details.
        * `area_uuid`: Unique identifier of the area.
        * `project_uuid`: Unique identifier of the project.
        * `name`: Name of the area.
     
### 2.2. Create Area

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "create",
      "data": {
          "name": "Area 1",
          "isolated": false
       }
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "create").
    * `data`: Area details.
        * `name`: Name of the area.
        * `isolated`: if you set isolated true,your area network is isolate.

     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/E/ACTION`
* **Response Payload:**

    ```json
    {
       "message":"success",
       "version":"v1.0",
       "action":"create",
       "data":{
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0",
          "name":"Area 1",
          "project_uuid":"7346d2b3-ee78-4907-b6cb-c936b8aed1b1"
       }
    }
    ```

    * `message`: Status of the request (e.g., "success").
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Area details.
        * `area_uuid`: Unique identifier of the area.
        * `project_uuid`: Unique identifier of the project.
        * `name`: Name of the area.
     
### 2.3. Edit Area

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "edit",
      "data": {
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0",
          "name": "Area 1",
          "isolated": false
       }
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "edit").
    * `data`: Area details.
        * `name`: Name of the area.
        * `isolated`: if you set isolated true,your area network is isolate.
        * `area_uuid`: Unique identifier of the area.
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/E/ACTION`
* **Response Payload:**

    ```json
    {
       "message":"success",
       "version":"v1.0",
       "action":"edit",
       "data":{
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0",
          "name":"Area 1",
          "project_uuid":"7346d2b3-ee78-4907-b6cb-c936b8aed1b1"
       }
    }
    ```

    * `message`: Status of the request (e.g., "success").
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Area details.
        * `area_uuid`: Unique identifier of the area.
        * `project_uuid`: Unique identifier of the project.
        * `name`: Name of the area.
     
### 2.4. Delete Area

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "delete",
      "data": {
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0"
       }
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "edit").
    * `data`: Area details.
        * `area_uuid`: Unique identifier of the area.
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/E/ACTION`
* **Response Payload:**

    ```json
    {
       "message":"success",
       "version":"v1.0",
       "action":"delete",
       "data":{
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0"
       }
    }
    ```

    * `message`: Status of the request (e.g., "success").
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Area details.
        * `area_uuid`: Unique identifier of the area.
     
### 2.5. Get All Zones

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "get-all-zones",
      "limit": 10,
      "offset": 0,
     "data":{
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0"
       }
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "get-all-zones").
    * `limit`: (Optional) Maximum number of zones to return. Default: 50.
    * `offset`: (Optional) Starting position for the results. Default: 0.
    * `data`: Area details.
        * `area_uuid`: Unique identifier of the area.
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/E/ACTION`
* **Response Payload:**

    ```json
    {
      "message": "success",
      "version": "v1.0",
      "action": "get-all-zones",
      "data": [
        {
          "zone_address": 50646,
          "name": "First zone",
          "area_uuid": "f1677ff1-0138-47a0-b202-5de5e83827a0",
          "area_name": "A514 office",
          "zone_uuid": "63ab9c4b-08f3-437e-a448-0eab7c9e1420"
        }
      ]
    }
    ```

    * `message`: Status of the request.
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Array of zone objects.
        * `zone_address`: Address of the zone.
        * `name`: Name of the zone.
        * `area_uuid`: Unique identifier of the area.
        * `area_name`: Name of the area.
        * `zone_uuid`: Unique identifier of the zone.
     
### 2.6. Get All Nodes

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "get-all-nodes",
      "limit": 10,
      "offset": 0,
     "data":{
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0"
       }
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "get-all-nodes").
    * `limit`: (Optional) Maximum number of nodes to return. Default: 50.
    * `offset`: (Optional) Starting position for the results. Default: 0.
    * `data`: Area details.
        * `area_uuid`: Unique identifier of the area.

* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/E/ACTION`
* **Response Payload:**

    ```json
    {
        "message": "success",
        "version": "v1.0",
        "action": "get-all-nodes",
        "data": [
            {
                "node_uuid": "bbcc84f7-0316-4ec6-0000-000000000000",
                "name": "LYTIVA_164EC6",
                "pid": "1015",
                "vid": "0263",
                "unicast_address": 5743,
                "zone_uuid": "63ab9c4b-08f3-437e-a448-0eab7c9e1420",
                "zone_name": "First zone",
                "zone_address": 50646,
                "model_id": "1303",
                "device_type": "ctl"
            },
            {
                "node_uuid": "bbcc84f7-0316-3716-0000-000000000000",
                "name": "LYTIVA_163716",
                "pid": "1015",
                "vid": "0263",
                "unicast_address": 1345,
                "zone_uuid": "06168eeb-7ca5-49e7-a769-7073347af48f",
                "zone_name": "Second Zone",
                "zone_address": 49536,
                "model_id": "1303",
                "device_type": "ctl"
            }
        ]
    }
    ```

    * `message`: Status of the request.
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Array of node objects.
        * `node_uuid`: Unique identifier for the node
        * `name`: Name of the node.
        * `zone_address`: Address of the zone.
        * `pid`: Product id
        * `vid`: Version id
        * `unicast_address`: Node unicast address
        * `zone_uuid`: Unique identifier of the zone.
        * `zone_name`: Zone name
        * `zone_address`: Zone address
        * `model_id`: Model identifier
        * `device_type`: Type of device
        * 

### 2.7. Get All Gateways

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "get-all-gateways",
      "limit": 10,
      "offset": 0,
       "data":{
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0"
       }
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "get-all-nodes").
    * `limit`: (Optional) Maximum number of nodes to return. Default: 50.
    * `offset`: (Optional) Starting position for the results. Default: 0.
    * `data`: Area details.
        * `area_uuid`: Unique identifier of the area.
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/E/ACTION`
* **Response Payload:**

    ```json
    {
       "message": "success",
       "version": "v1.0",
       "action": "get-all-gateways",
       "data": [
           {
               "gateway_uuid": "aaaa84f7-036e-8d2e-0000-000000000000",
               "name": "AERIVA_6E8D2E",
               "pid": "1041",
               "vid": "0111",
               "area_uuid": "f1677ff1-0138-47a0-b202-5de5e83827a0",
               "area_name": "A514 office",
               "unicast_address": 249
           }
       ]
   }
   ```

    * `message`: Status of the request.
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Array of gateway objects.
        * `gateway_uuid`: Unique identifier for the gateway
        * `name`: Name of the gateway.
        * `pid`: Product id
        * `vid`: Version id
        * `unicast_address`: Gateway unicast address
        * `area_uuid`: Unique identifier of the area.
        * `area_name`: Area name
     
## 3. Zone Actions

### 3.1. Get Zone

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "get",
      "data": {
          "zone_uuid": "63ab9c4b-08f3-437e-a448-0eab7c9e1420"
       }
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "get").
    * `data`: Zone details.
        * `zone_uuid`: Unique identifier of the zone.
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/E/ACTION`
* **Response Payload:**

    ```json
    {
       "message":"success",
       "version":"v1.0",
       "action":"get",
       "data":{
          "zone_uuid":"63ab9c4b-08f3-437e-a448-0eab7c9e1420",
          "zone_address":50646,
          "name":"First zone",
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0",
          "area_name":"A514 office"
       }
    }
    ```

    * `message`: Status of the request.
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Zone details.
        * `zone_address`: Address of the zone.
        * `name`: Name of the zone.
        * `area_uuid`: Unique identifier of the area.
        * `area_name`: Name of the area.
        * `zone_uuid`: Unique identifier of the zone.
     
### 3.2. Create Zone

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "create",
      "data": {
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0",
          "name": "Demo 1",
          "isolated": false
       }
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "create").
    * `data`: Zone details.
        * `area_uuid`: Unique identifier of the area.
        * `name`: Name of the area.
        * `isolated`: if you set isolated true,your zone network is isolate.

* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/E/ACTION`
* **Response Payload:**

    ```json
    {
       "action":"create",
       "message":"success",
       "version":"v1.0",
       "data":{
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0",
          "area_name":"A514 office",
          "zone_uuid":"57fc8ee9-b192-475f-8b59-8fef66838dfd",
          "zone_address":49442,
          "name":"Demo 1"
       }
    }
    ```

    * `message`: Status of the request.
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Zone details.
        * `zone_address`: Address of the zone.
        * `name`: Name of the zone.
        * `area_uuid`: Unique identifier of the area.
        * `area_name`: Name of the area.
        * `zone_uuid`: Unique identifier of the zone.
     
### 3.3. Edit Zone

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "edit",
      "data": {
          "zone_uuid":"57fc8ee9-b192-475f-8b59-8fef66838dfd",
          "name": "Hello 1",
          "isolated": false
       }
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "edit").
    * `data`: Zone details.
        * `name`: Name of the zone.
        * `isolated`: if you set isolated true,your zone network is isolate.
        * `zone_uuid`: Unique identifier of the zone.
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/E/ACTION`
* **Response Payload:**

    ```json
    {
       "message":"success",
       "action":"edit",
       "version":"v1.0",
       "data":{
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0",
          "area_name":"A514 office",
          "zone_uuid":"57fc8ee9-b192-475f-8b59-8fef66838dfd",
          "zone_address":49442,
          "name":"Hello 1"
       }
    }
    ```

    * `message`: Status of the request.
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Zone details.
        * `zone_address`: Address of the zone.
        * `name`: Name of the zone.
        * `area_uuid`: Unique identifier of the area.
        * `area_name`: Name of the area.
        * `zone_uuid`: Unique identifier of the zone.
     
### 3.4. Delete Zone

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "delete",
      "data": {
          "zone_uuid":"57fc8ee9-b192-475f-8b59-8fef66838dfd"
       }
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "delete").
    * `data`: Zone details.
        * `zone_uuid`: Unique identifier of the Zone.
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/E/ACTION`
* **Response Payload:**

    ```json
    {
       "action":"delete",
       "message":"success",
       "version":"v1.0",
       "data":{
          "zone_uuid":"57fc8ee9-b192-475f-8b59-8fef66838dfd",
          "zone_address":49442
       }
    }
    ```

    * `message`: Status of the request.
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Zone details.
        * `zone_uuid`: Unique identifier of the zone.
        * `zone_address`: Address of the zone.
     
### 3.5. Get All Nodes

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "get-all-nodes",
      "limit": 10,
      "offset": 0,
     "data":{
          "zone_uuid":"63ab9c4b-08f3-437e-a448-0eab7c9e1420"
       }
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "get-all-nodes").
    * `limit`: (Optional) Maximum number of nodes to return. Default: 50.
    * `offset`: (Optional) Starting position for the results. Default: 0.
    * `data`: Zone details.
        * `zone_uuid`: Unique identifier of the zone.

* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/E/ACTION`
* **Response Payload:**

    ```json
    {
       "message":"success",
       "version":"v1.0",
       "action":"get-all-nodes",
       "data":[
          {
             "node_uuid":"bbcc84f7-0316-4ec6-0000-000000000000",
             "name":"LYTIVA_164EC6",
             "pid":"1015",
             "vid":"0263",
             "unicast_address":5743,
             "zone_uuid":"63ab9c4b-08f3-437e-a448-0eab7c9e1420",
             "zone_name":"First zone",
             "zone_address":50646,
             "model_id":"1303",
             "device_type":"ctl"
          }
       ]
    }
    ```

    * `message`: Status of the request.
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Array of node objects.
        * `node_uuid`: Unique identifier for the node
        * `name`: Name of the node.
        * `pid`: Product id
        * `vid`: Version id
        * `unicast_address`: Node unicast address
        * `zone_uuid`: Unique identifier of the zone.
        * `zone_name`: Zone name
        * `zone_address`: Zone address
        * `model_id`: Model identifier
        * `device_type`: Type of device
     
### 3.6. Get Zone Added Gateways

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "get-added-gateways",
      "limit": 10,
      "offset": 0,
     "data":{
          "zone_uuid":"63ab9c4b-08f3-437e-a448-0eab7c9e1420"
       }
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "get-added-gateways").
    * `limit`: (Optional) Maximum number of nodes to return. Default: 50.
    * `offset`: (Optional) Starting position for the results. Default: 0.
    * `data`: Zone details.
        * `zone_uuid`: Unique identifier of the zone.

* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/E/ACTION`
* **Response Payload:**

    ```json
    {
       "message":"success",
       "version":"v1.0",
       "action":"get-added-gateways",
       "data":[
          {
             "gateway_uuid":"aaaa84f7-036e-8d2e-0000-000000000000",
             "name":"AERIVA_6E8D2E",
             "pid":"1041",
             "vid":"0111",
             "unicast_address":249,
             "zone_uuid":"63ab9c4b-08f3-437e-a448-0eab7c9e1420",
             "zone_name":"First zone",
             "zone_address":50646
          }
       ]
    }
    ```

    * `message`: Status of the request.
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Array of gateways objects.
        * `gateway_uuid`: Unique identifier for the gateway
        * `name`: Name of the gateway.
        * `pid`: Product id
        * `vid`: Version id
        * `unicast_address`: gateway unicast address
        * `zone_uuid`: Unique identifier of the zone.
        * `zone_name`: Zone name
        * `zone_address`: Zone address
     
## 4. Node Actions

### 4.1. Get Node

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "get",
      "data": {
          "node_uuid": "f1677ff1-0138-47a0-b202-5de5e83827a0"
       }
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "get").
    * `data`: Node details.
        * `node_uuid`: Unique identifier of the node.
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/E/ACTION`
* **Response Payload:**

    ```json
    {
       "message":"success",
       "version":"v1.0",
       "action":"get",
       "data":{
          "node_uuid":"bbcc84f7-0316-34c6-0000-000000000000",
          "name":"LYTIVA_1634C6",
          "pid":"1015",
          "vid":"0263",
          "unicast_address":2753,
          "zone_uuid":"3f669f5c-9355-4797-b2c7-43755d2bd33c",
          "zone_name":"Sixth zone",
          "zone_address":51276,
          "model_id":"1303",
          "device_type":"ctl"
       }
    }
    ```

    * `message`: Status of the request.
    * `version`: API version.
    * `action`: Action performed.
    * `data`: node objects.
        * `node_uuid`: Unique identifier for the node
        * `name`: Name of the node.
        * `pid`: Product id
        * `vid`: Version id
        * `unicast_address`: Node unicast address
        * `zone_uuid`: Unique identifier of the zone.
        * `zone_name`: Zone name
        * `zone_address`: Zone address
        * `model_id`: Model identifier
        * `device_type`: Type of device
     
## 5. Gateway Actions

### 5.1. Get Gateway

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/GATEWAY/ACTION`
* **Request Payload:**

    ```json
    {
      "version": "v1.0",
      "action": "get",
      "data": {
          "gateway_uuid": "f1677ff1-0138-47a0-b202-5de5e83827a0"
       }
    }
    ```

    * `version`: API version.
    * `action`: Action to perform (e.g., "get").
    * `data`: Gateway details.
        * `gateway_uuid`: Unique identifier of the gateway.
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/GATEWAY/E/ACTION`
* **Response Payload:**

    ```json
    {
       "message": "success",
       "version": "v1.0",
       "action": "get",
       "data": {
          "gateway_uuid": "aaaa84f7-036e-8d2e-0000-000000000000",
          "name": "AERIVA_6E8D2E",
          "pid": "1041",
          "vid": "0111",
          "area_uuid": "f1677ff1-0138-47a0-b202-5de5e83827a0",
          "area_name": "A514 office",
          "unicast_address": 249
       }
    }
    ```

    * `message`: Status of the request.
    * `version`: API version.
    * `action`: Action performed.
    * `data`: gateway object.
        * `gateway_uuid`: Unique identifier for the gateway
        * `name`: Name of the gateway.
        * `pid`: Product id
        * `vid`: Version id
        * `unicast_address`: Gateway unicast address
        * `area_uuid`: Unique identifier of the area.
        * `area_name`: Area name
     
## 6. Zone Operations

### 6.1. Get CCT Zone Status

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/STATUS`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "ctl",
       "address": 50646
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "ctl") .
    * `address`: Zone address
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/E/STATUS`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "ctl",
       "address": 50646,
       "ctl": {
          "lightness": 40,
          "temperature": 100
       }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Zone address
    * `ctl`: ctl objects.
        * `lightness`: Zone lightness
        * `temperature`: Zone temperature.
     
### 6.2. Get Dimmer Zone Status

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/STATUS`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "lightness",
       "address": 50646
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "lightness") .
    * `address`: Zone address
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/E/STATUS`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "lightness",
       "address": 50646,
       "lightness": {
          "lightness": 40,
       }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Zone address
    * `lightness`: lightness objects.
        * `lightness`: Zone lightness
     
### 6.3. Get Presence Sensor Zone Status

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/STATUS`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "presence-sensor",
       "address": 50646
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "presence-sensor") .
    * `address`: Zone address
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/E/STATUS`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "presence-sensor",
       "address": 50646,
       "presence-sensor": {
          "lightness": 40,
          "event": 1
       }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Zone address
    * `presence-sensor`: Presence sensor objects.
        * `lightness`: Zone lightness
        * `event`: Indicates whether there is an event within the zone or not.
     
### 6.4. Control CCT Zone

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/CONTROL`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "ctl",
       "address": 50646,
       "lightness": 10,
       "temperature": 100
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "ctl") .
    * `address`: Zone address
    * `lightness`: Set zone lightness
    * `temperature`: Set zone temperature
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/E/CONTROL`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "ctl",
       "address": 50646,
       "ctl": {
          "lightness": 40,
          "temperature": 100
       }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Zone address
    * `ctl`: ctl objects.
        * `lightness`: Zone lightness
        * `temperature`: Zone temperature.
     
### 6.5. Control Dimmer Zone

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/CONTROL`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "lightness",
       "address": 50646,
       "lightness": 40
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "lightness") .
    * `address`: Zone address
    * `lightness`: Set zone lightness
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/E/CONTROL`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "lightness",
       "address": 50646,
       "lightness": {
          "lightness": 40,
       }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Zone address
    * `lightness`: lightness objects.
        * `lightness`: Zone lightness
     
### 6.6. Get Entery Exit Sensor Zone Status

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/STATUS`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "entry-exit-sensor",
       "address": 50646
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "entry-exit-sensor") .
    * `address`: Zone address
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/E/STATUS`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "entry-exit-sensor",
       "address": 50646,
       "entry-exit-sensor": {
             "lightness": 55,
             "event": 1,
             "person_count": 3
          }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Zone address
    * `entry-exit-sensor`: Entry exist sensor objects.
        * `lightness`: Zone lightness
        * `event`: Indicates whether there is an event within the zone or not.
        * `person_count`: The counts show how many people have entered the zone.
     
### 6.7. Get Lux Sensor Zone Status

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/STATUS`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "lux-sensor",
       "address": 51535
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "lux-sensor") .
    * `address`: Zone address
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/E/STATUS`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "lux-sensor",
       "address":51535,
       "lux-sensor": {
             "lux_level": 1200
          }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Zone address
    * `lux-sensor`: Lux sensor objects.
        * `lux_level`: Shows the current lux level within the zone.
     
### 6.8. Get Temperature Humidity Sensor Zone Status

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/STATUS`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "temperature-humidity-sensor",
       "address": 51982
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "temperature-humidity-sensor") .
    * `address`: Zone address
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/ZONE/E/STATUS`
* **Response Payload:**

    ```json
    {
       "version":"v1.0",
       "message":"success",
       "type":"temperature-humidity-sensor",
       "address":51982,
       "temperature-humidity-sensor": {
                            "temperature":30,
                            "humidity":44
       }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Zone address
    * `temperature-humidity-sensor`: Temperature humidity sensor objects.
        * `temperature`: Shows how much temperature is inside the zone.
        * `humidity`: Shows how much humidity is inside the zone.

     
## 7. Node Operations

### 7.1. Get CCT Node Status

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/STATUS`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "ctl",
       "address": 50646
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "ctl") .
    * `address`: Node address
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/E/STATUS`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "ctl",
       "address": 50646,
       "ctl": {
          "lightness": 40,
          "temperature": 100
       }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Node address
    * `ctl`: ctl objects.
        * `lightness`: Node lightness
        * `temperature`: Node temperature.
     
### 7.2. Get Dimmer Node Status

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/STATUS`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "lightness",
       "address": 50646
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "lightness") .
    * `address`: Node address
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/E/STATUS`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "lightness",
       "address": 50646,
       "lightness": {
          "lightness": 40,
       }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Node address
    * `lightness`: lightness objects.
        * `lightness`: Node lightness
     
### 7.3. Control CCT Node

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/CONTROL`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "ctl",
       "address": 50646,
       "lightness": 10,
       "temperature": 100
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "ctl") .
    * `address`: Node address
    * `lightness`: Set node lightness
    * `temperature`: Set node temperature
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/E/CONTROL`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "ctl",
       "address": 50646,
       "ctl": {
          "lightness": 40,
          "temperature": 100
       }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Node address
    * `ctl`: ctl objects.
        * `lightness`: Node lightness
        * `temperature`: Node temperature.
     
### 7.4. Control Dimmer Node

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/CONTROL`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "lightness",
       "address": 50646,
       "lightness": 40
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "lightness") .
    * `address`: Node address
    * `lightness`: Set node lightness
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/E/CONTROL`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "lightness",
       "address": 50646,
       "lightness": {
          "lightness": 40,
       }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Node address
    * `lightness`: lightness objects.
        * `lightness`: Node lightness
     
### 7.5. Get Presence Sensor Node Status

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/STATUS`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "presence-sensor",
       "address": 1029
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "presence-sensor") .
    * `address`: Node address
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/E/STATUS`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "presence-sensor",
       "address": 1029,
       "presence-sensor": {
          "lightness": 40,
          "event": 1
       }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Node address
    * `presence-sensor`: Presence sensor objects.
        * `lightness`: Node lightness
        * `event`: Indicates whether the node has an event or not.
     
### 7.6. Get Entery Exit Sensor Node Status

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/STATUS`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "entry-exit-sensor",
       "address": 50646
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "entry-exit-sensor") .
    * `address`: Node address
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/E/STATUS`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "entry-exit-sensor",
       "address": 50646,
       "entry-exit-sensor": {
             "lightness": 55,
             "event": 1,
             "person_count": 3
          }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Node address
    * `entry-exit-sensor`: Entry exist sensor objects.
        * `lightness`: Node lightness
        * `event`: Indicates whether there is an event on the node.
        * `person_count`: Person counts
     
### 7.7. Get Lux Sensor Node Status

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/STATUS`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "lux-sensor",
       "address": 51535
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "lux-sensor") .
    * `address`: Node address
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/E/STATUS`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "lux-sensor",
       "address":51535,
       "lux-sensor": {
             "lux_level": 1200
          }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Node address
    * `lux-sensor`: Lux sensor objects.
        * `lux_level`: Displays the node's current lux level.
     
### 7.8. Get Temperature Humidity Sensor Node Status

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/STATUS`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "temperature-humidity-sensor",
       "address": 51982
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "temperature-humidity-sensor") .
    * `address`: Node address
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/E/STATUS`
* **Response Payload:**

    ```json
    {
       "version":"v1.0",
       "message":"success",
       "type":"temperature-humidity-sensor",
       "address":51982,
       "temperature-humidity-sensor": {
                            "temperature":30,
                            "humidity":44
       }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Node address
    * `temperature-humidity-sensor`: Temperature humidity sensor objects.
        * `temperature`: Shows what the temperature is.
        * `humidity`: Shows what the humidity is.
     
### 7.9. Get Parking Sensor Node Status

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/STATUS`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "type": "parking-sensor",
       "address": 51982
    }
    ```

    * `version`: API version.
    * `type`: Type to perform (e.g., "parking-sensor") .
    * `address`: Node address
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/NODE/E/STATUS`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "parking-sensor",
       "address": 3338,
       "parking-sensor": {
             "event":0
       }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type perform.
    * `address`: Node address
    * `parking-sensor`: Parking sensor objects.
        * `event`: Indicates whether there is an event on the parking sensor.
     
## 8. Gateway Operations

### 8.1. Get Gateway Status

* **Request Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/GATEWAY/STATUS`
* **Request Payload:**

    ```json
    {
       "version": "v1.0",
       "address": 249
    }
    ```

    * `version`: API version.
    * `address`: Gateway address
     
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/GATEWAY/E/STATUS`
* **Response Payload:**

    ```json
    {
       "version": "v1.0",
       "message": "success",
       "type": "gateway",
       "address": 249,
       "gateway": {
          "status": "online"
       }
    }
    ```
    * `version`: API version.
    * `message`: Status of the request.
    * `type`: Type gateway.
    * `address`: Gateway address
    * `gateway`: gateway objects.
        * `status`: indicates network connectivity, where `online` means connected and `offline` means disconnected.
     
## 9. Live Events
   If you want to work on live activity, you can subscribe to the following topics.

### 9.1. Edit Project
   If you are not using MQTT API and are editing projects from dashboard then you can subscribe to this topic.
   
* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/PROJECT/E/ACTION`
* **Response Payload:**

   ```json
   {
     "action": "edit",
     "message": "success",
     "version": "v1.0",
     "data": {
         "project_uuid": "7346d2b3-ee78-4907-b6cb-c936b8aed1b1",
         "name": "demo",
         "project_type": "Workspace"
      }
   }
   ```
   * `version`: API version.
   * `action`: Action performed.
   * `message`: Status of the request.
   * `data`:
      * `project_uuid`: The unique identifier of the project.
      * `name`: The updated name of the project.
      * `project_type`: The updated project type, ensuring it matches the supported types.
    
### 9.2. Delete Project
   If you delete the project from the dashboard, you can subscribe to this topic.   

* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/PROJECT/E/ACTION`
* **Response Payload:**

   ```json
   {
     "action": "delete",
     "message": "success",
     "version": "v1.0",
     "data": {
         "project_uuid": "7346d2b3-ee78-4907-b6cb-c936b8aed1b1"
      }
   }
   ```
   * `version`: API version.
   * `action`: Action performed.
   * `message`: Status of the request.
   * `data`:
      * `project_uuid`: The unique identifier of the project.
    
### 9.3. Create Area


* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/E/ACTION`
* **Response Payload:**

    ```json
    {
       "message":"success",
       "version":"v1.0",
       "action":"create",
       "data":{
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0",
          "name":"Area 1",
          "project_uuid":"7346d2b3-ee78-4907-b6cb-c936b8aed1b1"
       }
    }
    ```

    * `message`: Status of the request (e.g., "success").
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Area details.
        * `area_uuid`: Unique identifier of the area.
        * `project_uuid`: Unique identifier of the project.
        * `name`: Name of the area.
     
### 9.4. Edit Area


* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/E/ACTION`
* **Response Payload:**

    ```json
    {
       "message":"success",
       "version":"v1.0",
       "action":"edit",
       "data":{
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0",
          "name":"Area 1",
          "project_uuid":"7346d2b3-ee78-4907-b6cb-c936b8aed1b1"
       }
    }
    ```

    * `message`: Status of the request (e.g., "success").
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Area details.
        * `area_uuid`: Unique identifier of the area.
        * `project_uuid`: Unique identifier of the project.
        * `name`: Name of the area.
     
### 9.5. Delete Area

* **Response Topic:** `LYT/7346d2b3-ee78-4907-b6cb-c936b8aed1b1/AREA/E/ACTION`
* **Response Payload:**

    ```json
    {
       "message":"success",
       "version":"v1.0",
       "action":"delete",
       "data":{
          "area_uuid":"f1677ff1-0138-47a0-b202-5de5e83827a0"
       }
    }
    ```

    * `message`: Status of the request (e.g., "success").
    * `version`: API version.
    * `action`: Action performed.
    * `data`: Area details.
        * `area_uuid`: Unique identifier of the area.



