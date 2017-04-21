# *Creating a timetabling database using Neo4J*

# Introduction
This repository will contain documentation and work for my third year graph theory project in the course Computing and Software Development. The lecturer for this module is Ian Mcloughlin. I am required to design and prototype a Neo4j database for use in a timetabling system for a third level institute like GMIT which I am currently attending. The database should store information about student groups, classrooms, lecturers and class hours. 

# What is Neo4J?
Neo4j is the world's leading graph database. It is an open source NoSQL graph database implemented in java, hence the name Neo4java. It is described by its developers as an ACID (Atomicity, Consistency, Isolation, Durability) compliant transactional database with native graph storage and processing.

## what is a Graph Database?
A graph database is a database that uses graph structures for semantic queries with nodes, edges and properties to represent and store data. It is essentially a collection of nodes and edges. The key concept of the system is the graph (edge or relationship), which directly relates data items in the store. Each node represents an entity e.g. a person or business, and each edge represents a connection or relationship between two nodes. Every node in a graph database is defined by a unique identifier, a set of outgoing/incoming edges and a set of properties expressed as key/value pairs. Vice Versa with edges. 
### Benefits of a graph database
Graph databases are well suited for analysing interconnections, which is why there is been a lot of interest in using graph databases to mine data from social media websites. Graph databases are also useful for working with data in business disciplines that involve complex relationships and dynamic schema.

# Cypher

# Design
A graph database contains nodes, relationships, relationship types, labels and properties. The first thing I had to do was to come up with a design of the database. What would be nodes, what would be labels, which nodes had relationships and what would be properties. The database will be designed using the timetable of my current year as creating a timetabling database for all courses would be quite difficult. On a page I drew out a tree like structure of the database.

## Nodes
| Nodes | Properties |
| ------ | ------ |
| Course | courseId e.g. Software Development |
| Modules | name e.g. Graph Theory |
|  Years | year e.g. 3 |
|  Rooms | room e.g. G0994 |
| Lecturers | lecturer e.g. Dr Ian Mcloughlin |
| Groups | group e.g. A |
| Days | day e.g. Monday |
| Hours | hour e.g. 2pm |

### Load CSV
In order to get data such as rooms, modules, groups and lectures to use for the graph database, I first had to extract the data from GMIT's website by opening up the websites source code and taking out html tags containing the relevent data. I pasted the data into Notepad++ where I could use regular expression techniques to remove the html tags and clean up the data. The best way to import data into neo4j is by using CSV (Comma Seperated Values) files. To do this, I put the cleaned up data into microsoft excel and saved it as a CSV file. 

How to import data from a CSV file into neo4j:
```sh
LOAD CSV FROM 'file:///c:/rooms.csv' AS LINE CREATE (:Rooms {room: line.room})
```
or with headers
```sh
LOAD CSV WITH HEADERS FROM 'file:///c:/rooms.csv' AS LINE CREATE (:Rooms {room: line.room})
```