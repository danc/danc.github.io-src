Title: Premier contact avec Titan DB
tags: bigdata, graph

Quelques notes sur la mise en place de [Titan](http://titan.thinkaurelius.com/).

[Guide de démarrage](http://s3.thinkaurelius.com/docs/titan/1.0.0/getting-started.html)

## Installation de Java 8 ##

[Sur Ubuntu](https://doc.ubuntu-fr.org/java_proprietaire)

puis configuration de cette version par défaut :

        sudo update-alternatives --config java
        
## Installation de Titan ##

[Téléchargement](https://github.com/thinkaurelius/titan/wiki/Downloads)

        $ unzip titan-1.0.0-hadoop1.zip
        Archive:  titan-1.0.0-hadoop1.zip
        creating: titan-1.0.0-hadoop1/
        ...
        $ cd titan-1.0.0-hadoop1
        $ bin/gremlin.sh
        
                 \,,,/
                 (o o)
        -----oOOo-(3)-oOOo-----
        09:12:24 INFO  org.apache.tinkerpop.gremlin.hadoop.structure.HadoopGraph  - HADOOP_GREMLIN_LIBS is set to: /usr/local/titan/lib
        plugin activated: tinkerpop.hadoop
        plugin activated: aurelius.titan
        gremlin>
        
## Initialisation d'une base sur un backend BerkeleyDB ##

            gremlin> graph = TitanFactory.open('conf/titan-berkeleyje-es.properties')
            ==>standardtitangraph[berkeleyje:../db/berkeley]
            gremlin> GraphOfTheGodsFactory.load(graph)
            ==>null
            gremlin> g = graph.traversal()
            ==>graphtraversalsource[standardtitangraph[berkeleyje:../db/berkeley], standard]
            
## Initialisation d'une base sur un backend Cassandra ##

Note : Titan 1.0.0 semble compatible avec Cassandra 2.X [ref](http://www.datastax.com/2015/03/qa-cassandra-and-titandb-insights-into-datastaxs-graph-strategy).

Une version de cassandra et d'elasticsearch est fournie avec le téléchargement de Titan.

On les démarre :

            bin/cassandra -f
            bin/elastisearch
            gremlin> graph = TitanFactory.open('conf/titan-cassandra-es.properties')
                ==>standardtitangraph[cassandrathrift:[127.0.0.1]]
            gremlin> GraphOfTheGodsFactory.load(graph)
                ==>null
            gremlin> g = graph.traversal()
                ==>graphtraversalsource[standardtitangraph[cassandrathrift:[127.0.0.1]], standard]