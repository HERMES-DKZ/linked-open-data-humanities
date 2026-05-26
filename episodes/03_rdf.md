---
title: "Introduction to RDF and Basic Modeling"
teaching: 20
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- Why does LOD need a standard format like RDF?
- How does RDF structure information?
- What are blank nodes and literals?
- What are the limitations of N-Triples?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain the purpose of RDF and why standardization matters in LOD.
- Construct basic RDF triples in N-Triples format.
- Distinguish between IRIs, blank nodes, and literals, and know when to use each.

::::::::::::::::::::::::::::::::::::::::::::::::


## From the concept to RDF

In the previous chapters, we established two fundamental building blocks of Linked Open Data:

- The **subject-predicate-object model** as a way to break knowledge down into simple, structured statements.
- **IRIs** as a way to identify every resource and property unambiguously across the web.

We are now ready to combine these two ideas into a concrete, machine-readable format. But consider the following: imagine researchers in Tokyo, Cairo, and Berlin all model information about Vincent van Gogh using the subject-predicate-object structure, but each in their own way, with their own notation and their own rules for writing things down. Even if they all use IRIs, a computer cannot reliably process and combine their data if the formatting is inconsistent.

This is why we need not just a model, but a **standard**. A shared grammar that everyone follows, so that data from different sources can be read, understood, and connected by machines without human interpretation in between.

That standard is **RDF** (Resource Description Framework)** , a W3C standard for representing and exchanging knowledge on the web. It does not introduce new concepts, it takes the subject-predicate-object model and the use of IRIs that we already know, and defines precise, universally agreed rules for how to write them down.

Think of it like the rules of written language. Two people might know the same words, but without shared grammar and spelling conventions, written communication becomes unreliable. RDF is the grammar of Linked Open Data: it ensures that a triple written by a museum in Amsterdam means the same thing when read by someone in São Paulo.

By following RDF, datasets from entirely different institutions and domains can be linked together and queried as if they were one. At its core, every piece of information in RDF is expressed as a **triple**.

:::::::::::::::::::::::::::::::::::::: callout

### The RDF Triple

| Part | Role | Allowed values |
|---|---|---|
| **Subject** | The resource being described | IRI or blank node |
| **Predicate** | The relationship or property | IRI only |
| **Object** | The value or related resource | IRI, blank node, or literal |

The predicate is always an IRI. Relationships must be defined and unambiguous. The object can also be a concrete value (a literal) or a blank node, which we will look at below.

::::::::::::::::::::::::::::::::::::::::::::::::::


## Writing RDF: N-Triples

To write RDF data in a concrete, machine-readable way, we need a defined notation. The one we will use in this chapter is **N-Triples**.

In N-Triples, the rules are minimal:

:::::::::::::::::::::::::::::::::::::: callout

### Rules for writing N-Triples

* Write each triple on its own line
* Wrap every IRI in angle brackets: `< >`
* End every statement with a period: `.`
* Separate subject, predicate, and object with whitespace

::::::::::::::::::::::::::::::::::::::::::::::::::

Let us build a triple step by step. We want to express: *Wheatfield with Cypresses* was created by Vincent van Gogh.

**Step 1** — Identify subject, predicate, and object:

| Subject | Predicate | Object |
|---|---|---|
| *Wheatfield with Cypresses* | was created by | *Vincent van Gogh* |

**Step 2** — Replace each element with its Wikidata IRI:

| Subject | Predicate | Object |
|---|---|---|
| `https://www.wikidata.org/wiki/Q26221215` | `https://www.wikidata.org/wiki/Property:P170` | `https://www.wikidata.org/wiki/Q5582` |

**Step 3** — Write it as an N-Triple:

```
<https://www.wikidata.org/wiki/Q26221215> <https://www.wikidata.org/wiki/Property:P170> <https://www.wikidata.org/wiki/Q5582>.
```

A single triple is just one statement. In practice, many triples together form a **graph**, a network of connected resources. Recall the mind map from chapter 1: each arrow with two nodes was one triple. Written in N-Triples, the same information looks like this:

```
<https://www.wikidata.org/wiki/Q26221215> <https://www.wikidata.org/wiki/Property:P170> <https://www.wikidata.org/wiki/Q5582>.
<https://www.wikidata.org/wiki/Q5582> <https://www.wikidata.org/wiki/Property:P19> <https://www.wikidata.org/wiki/Q9883>.
<https://www.wikidata.org/wiki/Q9883> <https://www.wikidata.org/wiki/Property:P17> <https://www.wikidata.org/wiki/Q55>.
```

These three triples state that:

1. *Wheatfield with Cypresses* (`Q26221215`) was created by Vincent van Gogh (`Q5582`).
2. Vincent van Gogh (`Q5582`) was born in Zundert (`Q9883`).
3. Zundert (`Q9883`) is located in the Netherlands (`Q55`).

Notice that `Q5582` appears as both the object of the first triple and the subject of the second. This is how the graph connects: the same IRI in different positions links the triples together, creating a chain of related statements, exactly like the arrows in the mind map.


## Not Everything Is an IRI: Blank Nodes and Literals

So far, every part of our triples has been identified by an IRI. In practice, two other types of values appear in RDF: **blank nodes** and **literals**.

### Blank Nodes

A **blank node** is a resource without a globally unique identifier. It is used when an entity is relevant within the local dataset but does not need to be referenced from the outside world.

Imagine a painting in a museum's collection where the artist is unknown. We still want to record that there *was* a creator, we just cannot identify them. A blank node acts as an anonymous placeholder:

```
<https://www.wikidata.org/wiki/Q26221215> <https://www.wikidata.org/wiki/Property:P170> _:unknownArtist.
```

The prefix `_:` marks a blank node. The name after it (`unknownArtist`) is only meaningful within this file, it has no global significance and cannot be referenced from other datasets. Within the same dataset, however, the same blank node identifier can appear in multiple triples to make several statements about the same anonymous entity. For example, if we also know that this unknown artist was French, we can write:

```
<https://www.wikidata.org/wiki/Q26221215> <https://www.wikidata.org/wiki/Property:P170> _:unknownArtist.
_:unknownArtist <https://www.wikidata.org/wiki/Property:P27> <https://www.wikidata.org/wiki/Q142>.
```

Both triples refer to the same unnamed person, connected by the shared blank node identifier.

### Literals

A **literal** is a concrete value: a piece of text, a number, or a date. Unlike IRIs, literals do not point to a resource, they express a value directly.

For example, to record the creation year of *Wheatfield with Cypresses* or it's title:

```
<https://www.wikidata.org/wiki/Q26221215> <https://www.wikidata.org/wiki/Property:P571> "1889"^^<http://www.w3.org/2001/XMLSchema#gYear>.
<https://www.wikidata.org/wiki/Q26221215> <https://www.wikidata.org/wiki/Property:P1476> "Wheatfield with Cypresses".
```

The value `"1889"` is the literal. The part after `^^` is a **datatype IRI**.

:::::::::::::::::::::::::::::::::::::: callout

### Entities have no inherent properties

An entity in RDF is, at its core, nothing more than an IRI, a bare identifier. `https://www.wikidata.org/wiki/Q5582` does not "contain" the name *Vincent van Gogh*. It has no label, no birth year, no nationality built in. All of this information is added through triples, including the name itself:

```
<https://www.wikidata.org/wiki/Q5582> <https://www.wikidata.org/wiki/Property:P1476> "Vincent van Gogh"@en.
```

This is one of the central ideas of RDF: an entity is defined entirely by the statements made about it. The more triples you add, the richer the description becomes, but without any triples, an IRI is just an address pointing on an empty thing.

::::::::::::::::::::::::::::::::::::::::::::::::::

A computer, on its own, cannot know what `"1889"` means. Is it a year? A house number? A product code? The characters `1`, `8`, `8`, `9` are just a sequence of digits. The datatype IRI resolves this ambiguity: it tells the computer precisely how to interpret the value. `xsd:gYear` means "this is a calendar year", which allows the computer to sort or compare it correctly. For instance, it now knows that 1889 comes before 1900, or that it falls within the 19th century. Without the datatype, the computer would treat `"1889"` as plain text and could not do any of that.

The datatype IRIs come from a standardised vocabulary defining these. Common examples are `xsd:integer` for whole numbers, `xsd:date` for full dates like `"1853-03-30"`, and `xsd:string` for plain text. 

Plain text literals can omit the datatype. `"Wheatfield with Cypresses"` without any `^^` is valid and implicitly treated as plain text. 
They can also carry a **language tag** to specify which language they are written in:
```
<https://www.wikidata.org/wiki/Q26221215> <https://www.wikidata.org/wiki/Property:P1476> "Wheatfield with Cypresses"@en.
```
Here, no explicit `^^` datatype is needed. The language tag `@en` already tells the computer everything it needs to know about how to interpret the value: it is a piece of text in English. Language tag and datatype IRI cannot be combined on the same literal; they are two alternative ways of describing a value.


:::::::::::::::::::::::::::::::::::::: callout

### The three types of values in RDF

| Type | When to use | Syntax example |
|---|---|---|
| **IRI** | The resource has a global, persistent identifier | `<https://www.wikidata.org/wiki/Q5582>` |
| **Blank node** | The resource exists but has no global ID | `_:unknownArtist` |
| **Literal** | The value is text, a number, or a date | `"1889"^^<http://www.w3.org/2001/XMLSchema#gYear>` |

::::::::::::::::::::::::::::::::::::::::::::::::::


## Limitations of N-Triples

N-Triples is simple, strict, and easy to parse, but writing larger datasets in this format quickly becomes impractical. Every triple must repeat the full IRI of the subject, even when many consecutive triples describe the same resource. Consider these three statements about the same painting:

```
<https://www.wikidata.org/wiki/Q26221215> <https://www.wikidata.org/wiki/Property:P170> <https://www.wikidata.org/wiki/Q5582>.
<https://www.wikidata.org/wiki/Q26221215> <https://www.wikidata.org/wiki/Property:P571> "1889"^^<http://www.w3.org/2001/XMLSchema#gYear>.
<https://www.wikidata.org/wiki/Q26221215> <https://www.wikidata.org/wiki/Property:P1476> "Wheatfield with Cypresses"@en.
```

The IRI `https://www.wikidata.org/wiki/Q26221215` appears three times, once per triple. In a real dataset with hundreds or thousands of triples, this repetition makes files long, hard to read, and error-prone. How this problem is addressed in practice is the subject of the next chapter.

:::::::::::::::::::::::::::::::::::::: challenge  

## Exercise: From Mind Map to N-Triples

In the first chapter, you created a mind map from one of the following two texts. Now take the connections you modelled there and express them as N-Triples. For each arrow in your mind map, write one triple. Use Wikidata for all IRIs. For any entity not listed in the table below, look it up yourself on [Wikidata](https://www.wikidata.org). Try to include at least one literal (a year or a date).

---

**Group 1**: Vincent van Gogh was born in Zundert, the Netherlands, in 1853 and is a Post-Impressionist artist. In his youth, he developed a strong interest in art and initially studied in The Hague. He later moved to Paris, where he gained his first insights into modern art.

---

**Group 2**: Van Gogh created numerous famous paintings. The masterpiece ‘Starry Night’ was created in Saint-Remy-de-Provence and belongs to the Post-Impressionist era. The painting can be found in the Museum of Modern Art in Manhattan.

---

| Entity | Wikidata ID |
|---|---|
| Vincent van Gogh | `Q5582` |
| Zundert | `Q9883` |
| Netherlands | `Q55` |
| Paris | `Q90` |
| *Starry Night* | `Q45585` |
| Museum of Modern Art | `Q188740` |

| Property | Wikidata ID |
|---|---|
| place of birth | `P19` |
| country | `P17` |
| creator | `P170` |
| located in | `P276` |
| inception | `P571` |
| date of birth | `P569` |

:::::::::::::::: solution

There is no single correct answer, your solution depends on which connections you modelled in your mind map. The following are examples of valid triples for each group.

**Group 1**

```
<https://www.wikidata.org/wiki/Q5582> <https://www.wikidata.org/wiki/Property:P19> <https://www.wikidata.org/wiki/Q9883>.
<https://www.wikidata.org/wiki/Q9883> <https://www.wikidata.org/wiki/Property:P17> <https://www.wikidata.org/wiki/Q55>.
<https://www.wikidata.org/wiki/Q5582> <https://www.wikidata.org/wiki/Property:P569> "1853"^^<http://www.w3.org/2001/XMLSchema#gYear>.
```

**Group 2**

```
<https://www.wikidata.org/wiki/Q45585> <https://www.wikidata.org/wiki/Property:P170> <https://www.wikidata.org/wiki/Q5582>.
<https://www.wikidata.org/wiki/Q45585> <https://www.wikidata.org/wiki/Property:P276> <https://www.wikidata.org/wiki/Q188740>.
```

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::  


:::::::::::::::::::::::::::::::::::::: keypoints

- **RDF** is a W3C standard that gives a precise, shared format to the subject-predicate-object model.
- In RDF, every statement is a **triple**: subject, predicate, object.
- **N-Triples** is a notation for RDF: one triple per line, IRIs in angle brackets, statements ending with a period.
- The object of a triple can be an **IRI** (a resource), a **blank node** (an anonymous entity), or a **literal** (a concrete value like a date or string).

::::::::::::::::::::::::::::::::::::::::::::::::::
