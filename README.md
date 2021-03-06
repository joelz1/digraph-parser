# digraph-parser

Simple, standalone Java parser for digraph DSL (domain-specific language) in Graphviz DOT syntax.
Available on Maven Central: http://central.maven.org/maven2/com/paypal/digraph/digraph-parser/1.0/

[![Maven Central](https://img.shields.io/badge/maven%20central-1.0-brightgreen.svg)](http://search.maven.org/#artifactdetails|com.paypal.digraph|digraph-parser|1.0|)

See also
* http://www.graphviz.org/
* http://www.graphviz.org/doc/info/lang.html
* https://github.com/antlr/grammars-v4/tree/master/dot

#### Usage
```java
GraphParser parser = new GraphParser(new FileInputStream("src/test/resources/test1.dg"));
Map<String, GraphNode> nodes = parser.getNodes();
Map<String, GraphEdge> edges = parser.getEdges();	

log("--- nodes:");
for (GraphNode node : nodes.values()) {
	log(node.getId() + " " + node.getAttributes());
}

log("--- edges:");
for (GraphEdge edge : edges.values()) {
	log(edge.getNode1().getId() + "->" + edge.getNode2().getId() + " " + edge.getAttributes());
}
```

For following digraph the program produces output below:
```
digraph testgraph
{
 xxx [k=v]
 yyy [k1=v1 k2=v2]
 a -> b
 n1 [label="Node 1"]; n2 [label="Node 2"]; 
 n1 -> n2 [style=dotted label="A dotted edge"]
 n1 -> n4
 n2 -> n3
 n3 -> n5
 foo -> { bar baz } [ek=ev]
 foo -> bar [fbk=fbv]
 n4 -> n5
 bar [kk=vv]
 bar [kkk=vvv]
}
```

```
--- nodes:
a {}
b {}
bar {kk=vv, kkk=vvv}
baz {}
foo {}
n1 {label=Node 1}
n2 {label=Node 2}
n3 {}
n4 {}
n5 {}
xxx {k=v}
yyy {k1=v1, k2=v2}
--- edges:
a->b {}
foo->bar {fbk=fbv, ek=ev}
foo->baz {ek=ev}
n1->n2 {style=dotted, label=A dotted edge}
n1->n4 {}
n2->n3 {}
n3->n5 {}
n4->n5 {}
```

#### Maven dependency
```xml
<dependency>
  <groupId>com.paypal.digraph</groupId>
  <artifactId>digraph-parser</artifactId>
  <version>1.0</version>
</dependency>
```
