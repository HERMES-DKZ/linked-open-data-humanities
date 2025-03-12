---
title: "Introduction to RDF and Basic Modeling"
teaching: 20
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is RDF, and why is it used in Linked Open Data?
- How does RDF structure information using triples?
- How can we represent real-world relationships using RDF?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain the purpose and structure of RDF.
- Model basic relationships using the **subject-predicate-object** structure.
- Explain limitations of RDF

::::::::::::::::::::::::::::::::::::::::::::::::






RDF (Resource Description Framework) is a **universal data model** designed to represent relationships between entities in a structured way. It provides a **standardized format** for expressing knowledge using the **subject-predicate-object** model, which allows different datasets to be linked together and ensures interoperability.  

Using RDF, we can describe facts in a machine-readable way. Each RDF statement, called a **triple**, consists of:  

- **Subject**: The entity being described.  
- **Predicate**: The property or relationship between the subject and the object.  
- **Object**: The value or entity linked to the subject.  

For example, we can express the relationship between the painting *Wheatfield with Cypresses* and Vincent van Gogh using an RDF triple with URIs:  

```
<https://www.wikidata.org/wiki/Q26221215> <"was painted by"> <https://www.wikidata.org/wiki/Q5582>.
```

This triple means that *Wheatfield with Cypresses* was painted by Vincent van Gogh.  

### Using N-Triples as the Simplest RDF Representation  

The format used above is called **N-Triples**, which is the simplest, standardized way to represent RDF data. N-Triples is a line-based format where each fact is written on a single line in the form:  

```
<subject> <predicate> <object>.
```

This simplicity makes N-Triples easy to parse and store, making it ideal for exchanging RDF data between different systems.  

### RDF Properties and Vocabulary  

Beyond defining structured relationships, RDF also introduces **vocabularies** to standardize predicates. A vocabulary defines a set of properties and terms that describe specific concepts, ensuring consistency when linking data.  

For example, instead of every dataset using its own phrase for "was painted by," a standardized RDF vocabulary might define a property. For this property definition we could use wikidata, because they not only provide IRIs for Objects, but for properties aswell. There we find *[creator](https://www.wikidata.org/wiki/Property:P170)* , with the definition _maker of this creative work or other object_. Our whole triple would now look like this:

```
<https://www.wikidata.org/wiki/Q26221215> <https://www.wikidata.org/wiki/Property:P170> <https://www.wikidata.org/wiki/Q5582>
```

Such vocabularies enable different datasets to use the same terms, making data integration more efficient.  



### Blank Nodes and Literals in RDF  

In RDF, not every object needs a globally unique identifier (IRI). Sometimes, an entity exists that doesn’t need to be explicitly named—this is where **Blank Nodes** come in.  

A **Blank Node** represents an entity that exists in the data model but has no specific identifier. It is useful when:  
- The entity doesn’t have a meaningful global ID.  
- It is only relevant in a limited local context.  

For example, if a painting has an **unknown artist**, we might use a blank node to represent the missing information:  

```
<IRI for Unknown Painting> <IRI for "was painted by"> _:b1.
```

Here, `_:b1` is a blank node acting as a placeholder for an unknown artist.  

Additionally, RDF supports **Literals**, which represent concrete values such as **dates, numbers, or text** instead of links to other entities.  

For example, adding the creation year of *Wheatfield with Cypresses*:  

```
<https://www.wikidata.org/wiki/Q26221215> <"was painted in"> "1889"^^http://www.w3.org/2001/XMLSchema#integer.
```

This triple states that *Wheatfield with Cypresses* was painted in the year **1889**, with the data type explicitly set as an integer.  





:::::::::::::::::::::::::::::::::::::: challenge  

## Creating RDF Triples  

Convert the following statements into RDF triples using the correct structure. Use wikidata for IRIs and properties:  

1. Vincent van Gogh was born in Zundert.  
2. *Starry Night* was painted by Vincent van Gogh.  
3. The painting *The Potato Eaters* was created in 1885.  


:::::::::::::::: solution


```
TODO
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::  

