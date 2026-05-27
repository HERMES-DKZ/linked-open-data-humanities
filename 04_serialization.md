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



## Serialization Formats

So far, we have represented RDF as graphs. To store and exchange this information, the graph must be written down in a machine-readable text format. This process is called **serialization**.

A serialization format defines how RDF triples are written in a text file so that computers can read and process them.

One serialization format we have already seen is **N-Triples**. Files written in this format usually use the file extension `.nt`.

Another common serialization format is **Turtle** (Terse RDF Triple Language). Turtle is designed to be more compact and easier for humans to read and write than N-Triples. It reduces repetition. Turtle files usually use the file extension `.ttl`.

Example in N-Triple:


Example in Turtle:

### Basic Turtle Rules

1. Each triple ends with a period `.`
2. A semicolon `;` continues the same subject
3. A comma `,` continues the same subject and predicate



### Other Serialization Formats

Other common serialization formats are RDF/XML and JSON-LD. Although these formats look different, they all represent the same RDF graph.


Example in JSON-LD and RDF/XML 

```json

```

```xml

```
All RDF serialization formats are plain text formats and can be opened with any text editor.

::: callout

Each serialization formats has its own grammar ruleset, in the case of turtle you can find it here: https://www.w3.org/TR/turtle/

::::


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




## Namespaces and Prefixes

Namespaces help make RDF data unambiguous and interoperable. As introduced in the previous episode, IRIs uniquely identify resources such as people, places, or concepts.

However, full IRIs can become very long and difficult to read when used repeatedly in an RDF file. To make RDF easier to write and understand, we can define a short abbreviation for a namespace. This abbreviation is called a **prefix**.

Prefixes are declared at the beginning of a Turtle file using the `@prefix` keyword:

```turtle
@prefix wd: <https://www.wikidata.org/wiki/> .
```

For example, the following triple written with full IRIs:

```turtle
<https://www.wikidata.org/wiki/Q5582>
    <https://www.wikidata.org/wiki/Property:P19>
    <https://www.wikidata.org/wiki/Q9883> .
```

can be written more compactly using prefixes:

```turtle
@prefix wd: <https://www.wikidata.org/wiki/> .

wd:Q5582 wd:Property:P19 wd:Q9883 .
```

::::::::::::::::::::::::::::::::::::: challenge

## Find the mistakes in the following Turtle file

The following Turtle file contains several syntax mistakes. Copy the code snippet into a text editor and try to identify and correct the errors.

```turtle
1  @prefix wiki: <https://www.wikidata.org/wiki/> .
3  @prefix xsd: <http://www.w3.org/2001/XMLSchema#>

5  # Vincent van Gogh
6  wd:Q5582
7      ex:is ex:Artist ,
8      ex:hasName "Vincent van Gogh"^^xsd:string ;
9      ex:wasBornIn ex:Zundert ;
10     ex:wasBornInYear "1853"^^xsd:gYear ;
11     ex:hasArtMovement ex:PostImpressionism
12     ex:studiedIn ex:TheHague ;
13     ex:movedTo ex:Paris .

15 # Places
16 ex:Zundert
17     ex:isLocatedIn ex:Netherlands .

19 ex:TheHague
20     ex:isLocatedIn ex:Netherlands .

22 ex:Paris
23     ex:isLocatedIn ex:France ;

25 ex:SaintRemyDeProvence
26     ex:isLocatedIn ex:France .

28 ex:Manhattan
29     ex:isLocatedIn ex:USA .

31 # Artwork
32 wd:Q45585
33     ex:is ex:Painting ;
34     ex:hasName Starry Night^^xsd:string ;
35     ex:wasCreatedBy wd:Q5582 ;
36     ex:wasCreatedIn ex:SaintRemyDeProvence ;
37     ex:belongsTo ex:PostImpressionism ;
38     ex:isLocatedIn MuseumOfModernArt .

40 # Museum
41 ex:MuseumOfModernArt
42     ex:is ex:Museum ;
43     ex:isLocatedIn ex:Manhattan ;
44     ex:hasName "Museum of Modern Art"^^xsd:string .

46 # Art Movement
47 ex:PostImpressionism
48     ex:is ex:ArtMovement ;
49     ex:hasName "Post-Impressionism"^^xsd:string

```
:::::::::::::::: solution

There are 9 mistakes in the Turtle file:
- Missing prefix declaration: `@prefix ex: <http://example.org/> .`
- Wrong prefix name `wiki:` should be `wd:` 
- Missing `.` after the xsd: prefix declaration
- Comma used instead of semicolon in line 7
- Missing semicolon in line 11
- Incorrect punctuation in line 23: ; should be .
- Missing quatation marks around "Starry Night" in line 34
- Missing prefix `ex:` in line 38
- Missing final `.` in line 49

You can validate the Turtle file using an online Turtle editor or validator, for example:
(Turtle Web Editor)[https://felixlohmeier.github.io/turtle-web-editor/?utm_source=chatgpt.com]

The corrected Turtle file looks like this:

```turtle
@prefix ex: <http://example.org/> .
@prefix wd: <https://www.wikidata.org/wiki/> .
@prefix xsd: <http://www.w3.org/2001/XMLSchema#> .

# Vincent van Gogh
wd:Q5582
    ex:is ex:Artist ;
    ex:hasName "Vincent van Gogh"^^xsd:string ;
    ex:wasBornIn ex:Zundert ;
    ex:wasBornInYear "1853"^^xsd:gYear ;
    ex:hasArtMovement ex:PostImpressionism ;
    ex:studiedIn ex:TheHague ;
    ex:movedTo ex:Paris .

# Places
ex:Zundert
    ex:isLocatedIn ex:Netherlands .

ex:TheHague
    ex:isLocatedIn ex:Netherlands .

ex:Paris
    ex:isLocatedIn ex:France .

ex:SaintRemyDeProvence
    ex:isLocatedIn ex:France .

ex:Manhattan
    ex:isLocatedIn ex:USA .

# Artwork
wd:Q45585
    ex:is ex:Painting ;
    ex:hasName "Starry Night"^^xsd:string ;
    ex:wasCreatedBy wd:Q5582 ;
    ex:wasCreatedIn ex:SaintRemyDeProvence ;
    ex:belongsTo ex:PostImpressionism ;
    ex:isLocatedIn ex:MuseumOfModernArt .

# Museum
ex:MuseumOfModernArt
    ex:is ex:Museum ;
    ex:isLocatedIn ex:Manhattan ;
    ex:hasName "Museum of Modern Art"^^xsd:string .

# Art Movement
ex:PostImpressionism
    ex:is ex:ArtMovement ;
    ex:hasName "Post-Impressionism"^^xsd:string .

```

:::::::::::::::::::::::::
:::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::: callout

You do not need to memorize all RDF serialization formats. In practice, many tools can automatically convert between formats such as Turtle, RDF/XML, and JSON-LD.

Some useful online converters are:
- [EasyRDF Converter](https://www.easyrdf.org/converter)
- [RDF Converter by Zazuko](https://converter.zazuko.com/)

These tools are helpful for exploring different serialization formats and also validating RDF data.

::::::::::::

:::::: keypoints

- RDF graphs can be written in different serialization formats.
- Turtle is a compact and human-readable RDF serialization format.
- Turtle uses `.`, `;`, and `,` to structure RDF triples.
- Namespaces uniquely identify resources and properties.
- Prefixes shorten long IRIs and improve readability.

::::::