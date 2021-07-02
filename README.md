# Demo: Linked Data as generic Stigmergic Medium for Decentralized Coordination

The resources in this repository demonstrate how principles of stigmergy can be employed to coordinate a cyber-physical production scenario.
The algorithm that is implemented by the provided resources was originally published in the paper _**"Linked Data as generic Stigmergic Medium for Decentralized
Coordination"**, (T.Spieldenner, M.Chelli) ; ICSOFT 2021_ .

## Scenario and what is demonstrated

A (simulated) factory receives orders for simple IoT modules on a ”batch size 1” production line as commonly envisioned in Industry 4.0. Once an order is received, it is carried out by employing machines which provide the capabilities to perform manufacturing steps necessary for particular steps during the production process, e.g. providing plastic casts for casings, soldering electric circuits, or fixing the final model. Orders are executed by AI agents. The need for coordination arises as machines are shared between
simultaneously executed orders. The purpose of the presented coordination algorithm is to find a suitable distribution of machines between agents working on different orders, with the goal to complete each order in shortest possible time.



## Setup

### 1. Install Backends

1. Get AJAN-Service from https://github.com/aantakli/AJAN-service/
2. On commit https://github.com/aantakli/AJAN-service/commit/d27a54471e17f8adc30a1869e06cbe7ca7cc434f , install according to readme
3. Get the AJAN-Editor from https://github.com/aantakli/AJAN-editor
4. On commit https://github.com/aantakli/AJAN-editor/commit/ecd132eaae6cb025d3e60e2ec91351bbfa85ed79, install according to readme
5. Install Fuseki: https://jena.apache.org/documentation/fuseki2/

### 2. Import resources

1. Run AJAN by:
    1. `startTripleStore.bat`
    1. `startAJAN-loadTTL-false.bat`
3. Run editor according to readme
4. On tabs "Agents", select File -> Import Repository and select  `agents/agents.ttl` from this repo      
6. On tabs "Behavior", selct File -> Import BT, and via this, import both `behavior-trees/mark.ttl` and `behavior-trees/produce.ttl`
7. Open RDF4j Workbench: http://localhost:8090/workbench
    1. „Repositories“ -> „editor_data“
    2. Add“ -> Uncheck „use base URI as context identifier“ -> „RDF Data File“ -> select`queries/statements_stigmergy.trig` -> Upload
8. Create dataset in Fuseki:
    9. Access Fuseki on http://localhost:3030/
    10.  manage datasets“ -> „add new dataset“ 
    11.  Name: „stigmergy_production“, „Persistent“
    12.  „Home“ -> „add Data“ , select provided `domain/smartphone_wot.tll`, upload




## Running the scenario

1. Create Agents:
    1. In tabs "Agents", select "Instances"
    2. Click "+" to create a new Instance
    3. Select Template "MarkerAgent" and assign a name to the agent
    4. Repeat for the "Producer" Agent

2. Execute the marking algorithm
    1. Select the newly created "Marker" agent instance
    2. Scroll down to the "Send Message" dialogue field, and enter the following RDF snippet below
    3. Click the "Mail" Icon
    4. What you should observe: In the Fuseki Triple Store Model, you should find now newly created RDF that encodes stigmergy markers

```
@prefix order: <http://localhost:3030/orders/#>
@prefix mosaik: <http://www.mosaik-projekt.de/vocab/#>
<http://me> mosaik:ordered order:equippedModule .
```


## Acknowldegements

This work has been supported by the German Federal Ministry for Education and Research (BMBF) as part of the MOSAIK project (grant no. 01IS18070-C).
