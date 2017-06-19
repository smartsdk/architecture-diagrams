# FIWARE Architecture Diagrams
This repository include a collection of Architecture Diagrams in PUML and DOT to
support the documentation of FIWARE Architecture patterns in SmartSDK.

## Type of Diagrams

We basically use to type of diagrams:
* UML component diagrams to define logical
architecture of FIWARE Architecture Patterns (i.e. how the components plugs together).
Such diagrams are encoded using [PlantUML Syntax](http://plantuml.com/component-diagram).
* Directed Graphs to describe combination of FIWARE Architecture Patterns and Cloud Architecture Patterns, shifting from a logical architecture to a physical one (i.e. also covering deployment aspects of the components). Such diagrams are encoded using [DOT Language](http://www.graphviz.org/content/dot-language).

Such graphs can be easily rendered online with [gravizo](http://g.gravizo.com) or on a linux computer with [graphviz](http://www.graphviz.org).

## Examples

### FIWARE Reference Architecture Pattern for Data Management

```
@startuml;
skinparam componentStyle uml2

package "Data/Context Management Core" {
	interface NGSI
	NGSI -left- [Context Broker \n - Orion]
	NGSI -up- [CEP \n - Proton]

	NGSI -up- [CKAN]
	NGSI -up- [Stream Oriented \n- Kurento]
	package "Cosmos" {
		NGSI -up- [Cygnus]
		[Cygnus] -up- [Big Data Analysis]
		[Cygnus] -up- [STH Comet]
	}
}

@enduml
```

To render them using gravizo, it is simple as embedding the code in gravizo path:

```
https://g.gravizo.com/svg?
@startuml;
skinparam componentStyle uml2;

package "Data/Context Management Core" {;
	interface NGSI;
	NGSI -left- [Context Broker \n - Orion];
	NGSI -up- [CEP \n - Proton];

	NGSI -up- [CKAN];
	NGSI -up- [Stream Oriented \n- Kurento];
	package "Cosmos" {;
		NGSI -up- [Cygnus];
		[Cygnus] -up- [Big Data Analysis];
		[Cygnus] -up- [STH Comet];
	};
};

@enduml
```
Here is an example of resulting graph:

![Alt text](https://g.gravizo.com/svg?@startuml;skinparam%20componentStyle%20uml2;package%20"Data/Context%20Management%20Core"%20{;%20interface%20NGSI;%20NGSI%20-left-%20[Context%20Broker%20\n%20-%20Orion];%20NGSI%20-up-%20[CEP%20\n%20-%20Proton];%20NGSI%20-up-%20[CKAN];%20NGSI%20-up-%20[Stream%20Oriented%20\n-%20Kurento];%20package%20"Cosmos"%20{;%20%20NGSI%20-up-%20[Cygnus];%20%20[Cygnus]%20-up-%20[Big%20Data%20Analysis];%20%20[Cygnus]%20-up-%20[STH%20Comet];%20};};@enduml)

### SmartSDK HA Orion

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
