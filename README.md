# FIWARE & SMARTSDK Architecture Diagrams
This repository include a collection of architecture diagrams in PUML and DOT to
support the documentation of FIWARE Architecture and SmartSDK Deployment Architecture Pattern patterns.

## Type of Diagrams

We basically defined two type of diagrams:
* UML component diagrams to define FIWARE Reference Architecture Patterns, i.e. the logical architecture that depicts the interaction among components through their interfaces/APIs.
Such diagrams are encoded using [PlantUML Syntax](http://plantuml.com/component-diagram).
* Directed Graphs to describe the Reference Deployment Architecture Pattern as result of the combination of FIWARE Architecture Patterns and Cloud Architecture Patterns. Such diagrams shift the focus from a logical architecture to a physical one (i.e. also covering deployment aspects of the components) and are encoded using [DOT Language](http://www.graphviz.org/content/dot-language).

Architecture Patterns are meant to be modular. At such, you can build large patterns by composing smaller ones. See Examples.

Such graphs can be easily rendered online with [gravizo](http://g.gravizo.com) or on a linux computer with [graphviz](http://www.graphviz.org). If you use gravizo online rendering, you may need to transcode your DOT or PlantUML and end each line with ``;``. To avoid doing it manually, you can use the online [converter](https://g.gravizo.com/#converter).

## Examples

The repository includes several examples, here we discus few ones as guidelines for the for the development of additional examples.

### Example of Reference Architecture Pattern

Suppose that you have a pattern that include a FIWARE GE (e.g. ContextBroker) and a SmartSDK GE (e.g. NGSI Timeseries) that are interfaced through a NGSI API.


To specify that a component is FIWARE developed, you can use the following stereotype:

```SMARTSDK(timeseries,"NGSI TimeSeries",component)```

To specify that a component is SmartSDK developed, you can use the following stereotype:

```FIWARE(timeseries,"NGSI TimeSeries",component)```

Accordingly:

```
@startuml;
skinparam componentStyle uml2

!define ICONURL https://raw.githubusercontent.com/smartsdk/architecture-diagrams/smartsdk-template/dist
!includeurl ICONURL/common.puml
!includeurl ICONURL/fiware.puml
!includeurl ICONURL/smartsdk.puml

package "Example of Reference Architecture Pattern" {
	interface NGSI
	FIWARE(ctx,"Context Broker \n - Orion",component)
	SMARTSDK(timeseries,"NGSI TimeSeries",component)
	NGSI -left- ctx
  NGSI -right- timeseries
}
@enduml
```

Here is an example of resulting graph:

![Alt text](https://g.gravizo.com/svg?@startuml;skinparam%20componentStyle%20uml2;!define%20ICONURL%20https://raw.githubusercontent.com/smartsdk/architecture-diagrams/smartsdk-template/dist;!includeurl%20ICONURL/common.puml;!includeurl%20ICONURL/fiware.puml;!includeurl%20ICONURL/smartsdk.puml;package%20%22Example%20of%20Reference%20Architecture%20Pattern%22%20{;interface%20NGSI;FIWARE%28ctx,%22Context%20Broker%20\n%20-%20Orion%22,component%29;SMARTSDK%28timeseries,%22NGSI%20TimeSeries%22,component%29;NGSI%20-left-%20ctx;%20%20NGSI%20-right-%20timeseries;};@enduml)

Specific components that are not part of a pattern can be define using the standard PlantUML syntax:

```[External Component] -up- NGSI```

Here is the complete example:

```
@startuml;
skinparam componentStyle uml2

!define ICONURL https://raw.githubusercontent.com/smartsdk/architecture-diagrams/smartsdk-template/dist
!includeurl ICONURL/common.puml
!includeurl ICONURL/fiware.puml
!includeurl ICONURL/smartsdk.puml

package "Example of Reference Architecture Pattern" {
	interface NGSI
	FIWARE(ctx,"Context Broker \n - Orion",component)
	SMARTSDK(timeseries,"NGSI TimeSeries",component)
	NGSI -left- ctx
  NGSI -right- timeseries
}

[External Component] -up- NGSI

@enduml
```

Here is an example of resulting graph:

![Alt text](https://g.gravizo.com/svg?@startuml;skinparam%20componentStyle%20uml2;!define%20ICONURL%20https://raw.githubusercontent.com/smartsdk/architecture-diagrams/smartsdk-template/dist;!includeurl%20ICONURL/common.puml;!includeurl%20ICONURL/fiware.puml;!includeurl%20ICONURL/smartsdk.puml;package%20%22Example%20of%20Reference%20Architecture%20Pattern%22%20{;interface%20NGSI;FIWARE%28ctx,%22Context%20Broker%20\n%20-%20Orion%22,component%29;SMARTSDK%28timeseries,%22NGSI%20TimeSeries%22,component%29;NGSI%20-left-%20ctx;%20%20NGSI%20-right-%20timeseries;};[External%20Component]%20-up-%20NGSI;@enduml)

### FIWARE Reference Architecture Pattern for Data Management

This example present the FIWARE Reference Architecture Pattern for Data Management (cf. [github code](https://github.com/smartsdk/architecture-diagrams/blob/master/data-management/Data-ContextManagement.puml)).

```
@startuml;
skinparam componentStyle uml2

!define ICONURL https://raw.githubusercontent.com/smartsdk/architecture-diagrams/smartsdk-template/dist
!includeurl ICONURL/common.puml
!includeurl ICONURL/fiware.puml
!includeurl ICONURL/smartsdk.puml

package "Data/Context Management Core" {
	interface NGSI
	FIWARE(ctx,"Context Broker \n - Orion",component)
	FIWARE(cep,"CEP \n - Proton",component)
	FIWARE(ckan,"CKAN",component)
	FIWARE(kurento,"Stream Oriented \n- Kurento",component)
	NGSI -left- ctx
	NGSI -up- cep
	NGSI -up- ckan
	NGSI -up- kurento
	package "Cosmos" {
		FIWARE(cygnus,"Cygnus",component)
		FIWARE(bda,"Big Data Analysis",component)
		FIWARE(sth,"STH Comet",component)
		NGSI -up- cygnus
		cygnus -up- bda
		cygnus -up- sth
	}
}
@enduml
```

Here is an example of resulting graph:

![Alt text](https://g.gravizo.com/svg?@startuml;skinparam%20componentStyle%20uml2;!define%20ICONURL%20https://raw.githubusercontent.com/smartsdk/architecture-diagrams/smartsdk-template/dist;!includeurl%20ICONURL/common.puml;!includeurl%20ICONURL/fiware.puml;!includeurl%20ICONURL/smartsdk.puml;package%20"Data/Context%20Management%20Core"%20{;%20interface%20NGSI;%20FIWARE%28ctx,"Context%20Broker%20\n%20-%20Orion",component%29;%20FIWARE%28cep,"CEP%20\n%20-%20Proton",component%29;%20FIWARE%28ckan,"CKAN",component%29;%20FIWARE%28kurento,"Stream%20Oriented%20\n-%20Kurento",component%29;%20NGSI%20-left-%20ctx;%20NGSI%20-up-%20cep;%20NGSI%20-up-%20ckan;%20NGSI%20-up-%20kurento;%20package%20"Cosmos"%20{;%20%20FIWARE%28cygnus,"Cygnus",component%29;%20%20FIWARE%28bda,"Big%20Data%20Analysis",component%29;%20%20FIWARE%28sth,"STH%20Comet",component%29;%20%20NGSI%20-up-%20cygnus;%20%20cygnus%20-up-%20bda;%20%20cygnus%20-up-%20sth;%20};};@enduml)

### Combining different Architecture Patterns

Combining different PlantUML files representing different Architecture Patterns, its quite easy.

For example the typical Northbound / Southbound FIWARE Reference Architecture,
can be obtained by combining the FIWARE Reference Architecture Pattern for Data Management and FIWARE Reference Architecture Pattern for IoT Enablement (cf. [github code](https://github.com/smartsdk/architecture-diagrams/blob/master/southbound-northbound.puml)).

```
@startuml;
skinparam componentStyle uml2

!define BASEURL https://raw.githubusercontent.com/smartsdk/architecture-diagrams/master
!includeurl BASEURL/data-management/Data-ContextManagement.puml
!includeurl BASEURL/iot-management/IoT-Service-Enablement.puml

@enduml
```

Here is an example of resulting graph:

![Alt text](https://g.gravizo.com/svg?@startuml;skinparam%20componentStyle%20uml2;!define%20BASEURL%20https://raw.githubusercontent.com/smartsdk/architecture-diagrams/master;!includeurl%20BASEURL/data-management/Data-ContextManagement.puml;!includeurl%20BASEURL/iot-management/IoT-Service-Enablement.puml;@enduml)

### Example of SmartSDK Reference Deployment Architecture Pattern: HA Orion

This diagrams need still to be customized.

```
digraph G {
    rankdir=LR;
    compound=true;
    node [shape="record" style="filled"];
    splines=line;
    Client [fillcolor="aliceblue"];
    subgraph cluster {
      label="Docker Swarm Cluster";
      "Load Balancer" [fillcolor="aliceblue"];
      subgraph cluster_0 {
          label="Orion Context Broker stack";
          Orion1 [fillcolor="aliceblue"];
          Orion2 [fillcolor="aliceblue"];
          Orion3 [fillcolor="aliceblue"];
      }
      subgraph cluster_1 {
          label="MongoDB Replica Set stack";
          Mongo1 [fillcolor="aliceblue"];
          Mongo2 [fillcolor="aliceblue"];
          Mongo3 [fillcolor="aliceblue"];
      }
    }
    Client -> "Load Balancer" [lhead=cluster_0];
    "Load Balancer" -> {Orion1,Orion2,Orion3};
    Orion1 -> Mongo1 [lhead=cluster_1];
    Orion2 -> Mongo1 [lhead=cluster_1];
    Orion3 -> Mongo1 [lhead=cluster_1];
    Mongo1 -> {Mongo2, Mongo3} [dir="both"];
}
```

To render them using gravizo, it is simple as embedding the code in gravizo path:

```
https://g.gravizo.com/svg?
digraph G {
    rankdir=LR;
    compound=true;
    node [shape="record" style="filled"];
    splines=line;
    Client [fillcolor="aliceblue"];
    subgraph cluster {
      label="Docker Swarm Cluster";
      "Load Balancer" [fillcolor="aliceblue"];
      subgraph cluster_0 {
          label="Orion Context Broker stack";
          Orion1 [fillcolor="aliceblue"];
          Orion2 [fillcolor="aliceblue"];
          Orion3 [fillcolor="aliceblue"];
      }
      subgraph cluster_1 {
          label="MongoDB Replica Set stack";
          Mongo1 [fillcolor="aliceblue"];
          Mongo2 [fillcolor="aliceblue"];
          Mongo3 [fillcolor="aliceblue"];
      }
    }
    Client -> "Load Balancer" [lhead=cluster_0];
    "Load Balancer" -> {Orion1,Orion2,Orion3};
    Orion1 -> Mongo1 [lhead=cluster_1];
    Orion2 -> Mongo1 [lhead=cluster_1];
    Orion3 -> Mongo1 [lhead=cluster_1];
    Mongo1 -> {Mongo2, Mongo3} [dir="both"];
}
```

Here is an example of resulting graph:

![Alt text](https://g.gravizo.com/svg?digraph%20G%20{%20%20%20%20rankdir=LR;%20%20%20%20compound=true;%20%20%20%20node%20[shape="record"%20style="filled"];%20%20%20%20splines=line;%20%20%20%20Client%20[fillcolor="aliceblue"];%20%20%20%20subgraph%20cluster%20{%20%20%20%20%20%20label="Docker%20Swarm%20Cluster";%20%20%20%20%20%20"Load%20Balancer"%20[fillcolor="aliceblue"];%20%20%20%20%20%20subgraph%20cluster_0%20{%20%20%20%20%20%20%20%20%20%20label="Orion%20Context%20Broker%20stack";%20%20%20%20%20%20%20%20%20%20Orion1%20[fillcolor="aliceblue"];%20%20%20%20%20%20%20%20%20%20Orion2%20[fillcolor="aliceblue"];%20%20%20%20%20%20%20%20%20%20Orion3%20[fillcolor="aliceblue"];%20%20%20%20%20%20}%20%20%20%20%20%20subgraph%20cluster_1%20{%20%20%20%20%20%20%20%20%20%20label="MongoDB%20Replica%20Set%20stack";%20%20%20%20%20%20%20%20%20%20Mongo1%20[fillcolor="aliceblue"];%20%20%20%20%20%20%20%20%20%20Mongo2%20[fillcolor="aliceblue"];%20%20%20%20%20%20%20%20%20%20Mongo3%20[fillcolor="aliceblue"];%20%20%20%20%20%20}%20%20%20%20}%20%20%20%20Client%20->%20"Load%20Balancer"%20[lhead=cluster_0];%20%20%20%20"Load%20Balancer"%20->%20{Orion1,Orion2,Orion3};%20%20%20%20Orion1%20->%20Mongo1%20[lhead=cluster_1];%20%20%20%20Orion2%20->%20Mongo1%20[lhead=cluster_1];%20%20%20%20Orion3%20->%20Mongo1%20[lhead=cluster_1];%20%20%20%20Mongo1%20->%20{Mongo2,%20Mongo3}%20[dir="both"];})
