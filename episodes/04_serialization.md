---
title: "Serialization"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- How can RDF graphs be wirtten down in files?
- What are serialization formats?
- What is Turtle?
- What are namespaces and prefixes?


::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain the purpose of serialization formats
- Identify common serialization formats
- Read and write RDF in Turtle syntax
- Explain the purpose of namspaces and prefixes
- Identify namspaces and prefixes in a RDF file

::::::::::::::::::::::::::::::::::::::::::::::::



## Serialization formats

Serialisation is the process of converting our drawn graphs into a text form, this is writing them down in a file. This allows the computer to understand and process them. We have already learnt about one **serialisation format**: n-triple. If we were to save it as a file on our computer, the file would end in `.nt`.
Another serialisation format is Turtle (Terse RDF Triple Language), and these files end in `.ttt`

A serialisation format is the answer to the question of how to write things down in RDF so that the machine understands them. In short Turtle is an example for such a format.

Turtle example
```

##statements
```
Other common serialization formats:

* RDF/XML
* JSON-LD
* N-Triples




::::::::::::::::::::::::::::::::::::: challenge

## Write down the information in turtle

List some statements and ask the learners to transform them to valid turtle.

:::::::::::::::: solution


```
TODO
Valid turtle.
```

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::




## Namespaces

As described in the chapter ‘The Concept of IRIs’, namespaces are used to avoid ambiguity in resources. As they are frequently used in RDF files, this can be confusing for humans. It is therefore possible to assign a **prefix** – effectively an abbreviation – to a namespace once at the start of an RDF file using the line `@prefix ns: <fullnamespace>`. This abbreviation can then be used throughout the entire RDF file,  in which case the surrounding characters `<` and `>` of the resources are also no longer required. This abbreviation then applies only locally within that file.

Example: 
````
<https://www.wikidata.org/wiki/Q5582><https://www.wikidata.org/wiki/Property:P19><https://www.wikidata.org/wiki/Q9883>
````

````
@prefix wd: <https://www.wikidata.org/wiki/>.

wd:Q5582 wd:Property:P19 wd:Q9883 .
```
::::::::::::::::::::::::::::::::::::: challenge

## Find the mistakes in the following turtle file

A few spelling mistakes have crept into the following turtle file. Take a look at the code example and try to spot the mistakes.

```turtle

```
:::::::::::::::: solution


```
Valid turtle.
```

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::: callout

You do not have to know all the serialization Formats, there are plenty of converter tools on the web, for example the [EASYRDF Converter](https://www.easyrdf.org/converter) or the [RDF Converter by Zazuko](https://converter.zazuko.com/).

::::::::::::

:::::: keypoints

- How can RDF graphs be wirtten down in files?
- What are serialization formats?
- What is Turtle?
- What are namespaces and prefixes?
- Why are namspaces and prefixes used?

::::::