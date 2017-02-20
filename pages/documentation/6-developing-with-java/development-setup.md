---
title: Java Development Setup
keywords: java
last_updated: January 2017
tags: [java]
summary: "How to set up a Java GRAKN.AI environment."
sidebar: documentation_sidebar
permalink: /documentation/developing-with-java/java-setup.html
folder: documentation
---
{% include warning.html content="Please note that this page is in progress and subject to revision." %}

## Basic Setup

This section will discuss how to start developing with Grakn using the Java API. 
All Grakn applications require the following Maven dependency: 

```xml
<dependency>
    <groupId>ai.grakn</groupId>
    <artifactId>grakn-graph</artifactId>
    <version>${project.version}</version>
    </dependency>
```
    
This dependency will give you access to the Core API as well as an in-memory graph, which serves as a toy graph, should you wish to use the stack without having to have an instance of the Grakn server running.

## Server Dependent Setup

If you require persistence and would like to access the entirety of the Grakn stack, then it is vital to have an instance of engine running.  
Please see the [Setup Guide](../get-started/setup-guide.html) on more details on how to setup a Grakn server.

Depending on the configuration of the Grakn server, your Java application will require one of the following dependencies. When your server is running against a Titan backend: 

````xml   
<dependency>
    <groupId>ai.grakn</groupId>
    <artifactId>titan-factory</artifactId>
    <version>${project.version}</version> 
</dependency>
````    

When your server is running against a OrientDB backend:

```xml
<dependency>
    <groupId>ai.grakn</groupId>
    <artifactId>orientdb-factory</artifactId>
    <version>${project.version}</version> 
</dependency>
```    
    

{% include note.html content="The distribution package comes with a Titan backend configured out of the box. OrientDB support is still in early stages of development. " %}

## Initialising a Graph

You can initialise an in memory graph without having the Grakn server running with:  

```java
GraknGraph graph = Grakn.factory(Grakn.IN_MEMORY, "keyspace").getGraph();
```    
    
If you are running the Grakn server locally then you can initialise a graph with:

```java    
GraknGraph graph = Grakn.factory(Grakn.DEFAULT_URI, "keyspace").getGraph();
```
    
If you are running the Grakn server remotely you must initialise the graph by providing the IP address of your server:

```java
GraknGraph graph = Grakn.factory("127.6.21.2", "keyspace").getGraph();
```
    
The string "keyspace" uniquely identifies the graph and allows you to create different graphs.  

Please note that graph keyspaces are **not** case sensitive so the following two graphs are actually the same graph:

```java
    GraknGraph graph1 = Grakn.factory("127.6.21.2", "keyspace").getGraph();
    GraknGraph graph2 = Grakn.factory("127.6.21.2", "KeYsPaCe").getGraph();
```
   
All graphs are also singletons specific to their keyspaces so be aware that in the following case:

```java
   GraknGraph graph1 = Grakn.factory("127.6.21.2", "keyspace").getGraph();
   GraknGraph graph2 = Grakn.factory("127.6.21.2", "keyspace").getGraph();
   GraknGraph graph3 = Grakn.factory("127.6.21.2", "keyspace").getGraph();
```
  
any changes to `graph1`, `graph2`, or `graph3` will all be persisted to the same graph.

## Comments
Want to leave a comment? Visit <a href="https://github.com/graknlabs/docs/issues/23" target="_blank">the issues on Github for this page</a> (you'll need a GitHub account). You are also welcome to contribute to our documentation directly via the "Edit me" button at the top of the page.


{% include links.html %}
