---
title: "Model with Ontologies and Vocabularies"
teaching: 10
exercises: 2
---

::: questions
-   What steps you need to take to create an RDF data model from tabular data?
-   What is the difference between a resource and a concept?
-   What is RDF Schema used for and what does it include?
-   What are vocabularies and ontologies used for?
-   How to find vocabularies and ontologies?
-   How to apply RDF Schema and vocabularies to create a RDF datamodel?
:::

::: objectives
-   Identify entities and relationships in tabular data
-   Distinguish between resources, concepts, and literals
-   Explain the purpose of RDF Schema
-   Apply classes and properties to RDF data
-   Reuse existing vocabularies and ontologies
-   Create a simple RDF data model from tabular data
:::

## Planning the Data Model

After exploring the basic concepts and syntax of Linked Open Data, we will now work with a tabular museum dataset containing information about artworks from the Metropolitan Museum of Art (the Met).

Before we can create an RDF dataset, we first need to understand the structure of the data and build a conceptual data model (decide how the underlying data model will look). Although the dataset is presented as a table, each row contains information about several different entities at once.

Our task is to identify these entities, the relationships between them as well as the attributes of the entities, and gradually transform the tabular data into a RDF data model.

| objectID | museum | department | departmentID | accessionYear | objectName | title | artistRole | artistDisplayBio | artist | objectDate | city | country | classification | linkResource | tags | tag1 |
|----|----|----|----|----|----|----------|----|----|----|----|----|----|----|----|----|----|
| 693151 | Metropolitan Museum of Art | Drawings and Prints | 3 | 1978 | Print | The Dismissed Servant | Publisher | French, Paris ca. 1686–1762 Grand Vaux | Surugue, Louis | ca. 1749 | Berlin |  | Prints | http://www.metmuseum.org/art/collection/search/693151 | Women\|Servants | woman |
| 708926 | Metropolitan Museum of Art | Arts of Africa, Oceania, and the Americas | 2 | 2015 | Photograph | Woman outdoors – Ewe kente skirt, headtie and blouse | Photographer | Togolese, Kedzi 1880–1975 Lomé | Acolatse, Alex Agbaglo | 1975 | Lomé | Togo | Photographs | http://www.metmuseum.org/art/collection/search/708926 | Portraits\|Women | Portraits |

::: instructor
The lesson repository contains both a markdown and an HTML representation of the dataset:

-   [markdown representation](https://github.com/HERMES-DKZ/linked-open-data-humanities/blob/main/episodes/data/met-dataset-50.md)

-   [html representation](https://github.com/HERMES-DKZ/linked-open-data-humanities/blob/main/episodes/data/met-dataset-50.html)

Depending on the size of the group, learners can either inspect the table individually or work in small groups.
:::

### Entities and Attibutes

:::: discussion
Look at the dataset as a group, especially pay attention to the coloum headers.

Which different kinds of entities are described in the table?
Which columns seem to describe the same entities?

::: solution
The table contains information on three main entities. If we take the coloum headers these could be: museum, artworks and artists. The museum could include `museum`, `department` and `departmentID` or department could be seen as an indepentant entity; the artists includes `artist` `artist bio` and `artistrole`; and the artworks include, for example, `objectid`, `classification`, `title` and `tags`.

However, there are also columns that cannot be clearly assigned. For example, `city` and `country` may also refer to the artist or the artwork or could be seen as independant entities, whilst `accession year` only makes sense in relation to the artwork and the museum, and `artist role` in relation to both the artwork and the artist.

As always, modelling decisions are heavily influenced by interpretation.
:::
::::

We took the first step to identify the key entities in our dataset and started with distinguishing between entities and attributes, describing these. 

TODO: Add description of attriubutes.


:::: challenge
## Create a Mind Map out of the Tabular Dataset

Work in small groups and choose one row from the dataset. Use Excalidraw (https://excalidraw.com/) or a sheet of paper to build a mind map step by step.

1.  Think about what entities we identified earlier. Draw nodes for these entities and think about which table cell could represent them.  

2. Cluster the informations in the other table cells around these.

2.  How are the central nodes interconnected with the coloumn header? The column headers help you interpret the values.
    Use them to decide what the values represent.

3.  Name the relationships between the central nodes by assigning labels to the connections. Pay attention to the direction of the arrows.

Tip: Do not try to model everything at once. Start by identifying the main entities, then gradually add more detail.
::: solution
TODO: Add image of mindmap

1.  Central nodes are the ones where the most other nodes cluster around. For example: objectID, artist, department or museum. Keep in mind – Modeling decisions are subjective.

2.  The column headings provide context for the values in the table. For example, without the column header, an ObjectID would simply be a number. The column header tells us that the number refers to an artwork like `708926` → is a `ObjectID` in the context of our artwork. You can expand this process with the other coloumns as well: Similarly, the value "Photographer" in the `artistrole` column only becomes meaningful when we know that it refers to the creator of the artwork. The `Acolatse, Alex Agbaglo` is the `Photoprapher` of the artwork.

3.  Possible relationship labels include:

-   Museum → owns → ObjectID
-   Department → manages → ObjectID
-   Artist → created → ObjectID

:::instructor
Its always possible to turn around the statement.

-   ObjectID  → was created by → Artist
-   ObjectID → is owned by → Museum
-   ObjectID → is managed by → Department

::::

Other valid relationships may be possible depending on how the data is interpreted.
:::
::::

## Resources and Classes

The mind map already contains several interconnected nodes. We can now add another layer of meaning to the model.

The ObjectID does not simply represent a number. It refers to a specific artwork. Likewise, an artist name refers to a specific person.

In RDF, we call these identifiable things resources. Resources can also belong to broader categories.

```text
ObjectID693151 rdf:type Artwork
```

The artwork represented by ObjectID `693151` is an individual resource, while `Artwork` represents a more abstract concept the ressource belongs to, called a class.

This distinction between individual resources and classes is an important part of RDF modeling.

Think of `rdf:type` like a sticker or a name tag: it doesn't change the thing it's stuck on, it just tells whoever looks at it which drawer the thing belongs in. `ObjectID693151` stays exactly the artwork it was, but with a `rdf:type Artwork` sticker on it, everyone (and every machine) reading our data instantly knows: "ah, this one goes in the 'Artwork' drawer."

`rdf:type` is not something we had to invent ourselves, it already comes built into RDF, so every RDF tool understands it in exactly the same way, everywhere. That is the whole benefit: instead of everyone coming up with their own way of saying "this is a kind of that", there is exactly one standard sticker for it, and we can start using it immediately.

What does this actually buy us? Once things are sorted into drawers like this, we can start asking useful questions of our data: "show me everything in the Artwork drawer", or "show me everything in the Person drawer" - without writing any special code for it. The sorting itself already contains that information.

Not everything in our table refers to an identifiable thing, though. Values such as a date, a height in centimeters, or a free-text description are simply data values, there is nothing further we could point to or describe. In RDF, such values are called **literals**. A literal has no identity of its own; it is a plain piece of information attached to a resource, for example:

```text
ObjectID693151 hasTitle "The Dismissed Servant"
```

So when we look at the nodes in our data model, each one is one of the following:

- a **resource** - an identifiable thing (an artwork, an artist, a museum),
- a **literal** - a plain value (a date, a number, a string), or
- a **class** - a category that resources belong to (Artwork, Person, Museum).

:::: challenge
## Type your resources

Go back to the mind map you sketched earlier.

1. Pick three or four nodes from your mind map that you would classify as resources.
2. For each resource, write one simple triple that states which class it belongs to, using `rdf:type`. We have not reused any external vocabulary yet, so simply invent short placeholder terms of your own (e.g. `ex:Artwork`, `ex:Person`, `ex:Museum`).
3. Compare your triples with another group. Did you choose the same classes for the same kind of node?

::: solution

Possible triples for our example object `693151`:

```text
ex:ObjectID693151 rdf:type ex:Artwork
ex:SurugueLouis rdf:type ex:Person
ex:MetMuseum rdf:type ex:Museum
ex:DrawingsAndPrints rdf:type ex:Department
```

Different groups may pick different class names or a different level of detail (e.g. `ex:Artist` instead of `ex:Person`). This is completely normal. Modelling always involves choices and there is rarely a single correct answer.

:::
::::

## RDF Schema

With `rdf:type` alone, we can already sort our resources into drawers: an "Artwork" drawer, a "Person" drawer, a "Museum" drawer. But nothing yet stops us from putting the wrong thing into the wrong drawer. RDF itself would not complain if we accidentally wrote `ex:MetMuseum rdf:type ex:Person`, a museum sorted into the "Person" drawer. RDF has no way to say what may go into a drawer, or what a drawer even means. That is the gap RDF Schema (RDFS) closes.

You can picture RDFS as the label and instruction sheet on each drawer: it doesn't add any new artworks or people to our data, it explains what each drawer is for, what is allowed to go into it, and how the drawers relate to one another (for example, that the "Print" drawer sits inside the bigger "Artwork" drawer).

RDFS is, just like RDF, its own small vocabulary, it simply lives under its own prefix, `rdfs:`. The official specification is available at https://www.w3.org/TR/rdf11-schema/. It adds only a handful of terms, and they do two jobs.

**1. Naming and describing the drawers themselves**

* `rdfs:Class` - marks something as being a drawer (a class) at all, rather than an individual item. `ex:Artwork rdf:type rdfs:Class` says: "ex:Artwork is a drawer you can sort things into."
* `rdfs:Resource` - the biggest drawer of all; literally everything in RDF fits into it.
* `rdfs:Literal` - the drawer for plain values, like text, numbers, or dates.

**2. Writing rules for our properties**

* `rdfs:domain` - "who is allowed to use this connector?" E.g. `ex:createdBy rdfs:domain ex:Artwork` says only things from the Artwork drawer may have a creator.
* `rdfs:range` - "what is allowed on the other end of this connector?" E.g. `ex:createdBy rdfs:range ex:Person` says the creator must come from the Person drawer.
* `rdfs:subClassOf` - "this drawer sits inside a bigger drawer." E.g. `ex:Print rdfs:subClassOf ex:Artwork` means everything in the Print drawer automatically also counts as being in the Artwork drawer.
* `rdfs:label` - a friendly, readable name for a technical term, e.g. `ex:Artwork rdfs:label "Artwork"`.

What do we actually gain from this? Once we write `ex:createdBy rdfs:domain ex:Artwork` and `rdfs:range ex:Person`, a tool reading our data can automatically check whether it still makes sense. For example, flagging it if a museum, rather than a person, is ever entered as a creator. Just as importantly, anyone else picking up our data - a colleague, a reused dataset, another tool - can immediately see what each drawer and each connector is meant to be used for, without having to ask us. RDFS turns a private collection of guesses into a documented, shareable, checkable model.

The following challenges apply this in exactly this order: first sorting things into drawers, then writing the rules for the drawers.

:::: challenge
## Classify the nodes in the model

This challenge focuses on `rdfs:Resource`, `rdfs:Class`, and `rdfs:Literal`, deciding what *kind* of thing each node in your model is.

Look at the model you have built so far: the entities from your mind map, the classes you assigned to them with `rdf:type` in *Type your resources*, and any literals you have written down along the way (such as a title or a date).

For each node, decide whether it represents:

-   a resource,
-   a literal,
-   or a class.

Discuss your reasoning with your group.

::: solution

For our example object `693151`, a possible classification looks like this:

| Node | Type |
|---|---|
| `ex:ObjectID693151` | resource (an individual artwork) |
| `ex:Artwork` | class |
| `ex:SurugueLouis` | resource (an individual person) |
| `ex:Person` | class |
| `"The Dismissed Servant"` | literal (a title) |
| `"ca. 1749"` | literal (a date) |
| `ex:MetMuseum` | resource (an individual museum) |

A useful rule of thumb: if you could imagine writing further facts about a node (its birth date, its location, its opening hours), it is probably a resource. If a value simply *is* the fact, and cannot be described any further, it is a literal.

:::
::::

:::: challenge
## From rdf:type to a full RDFS model

This challenge focuses on `rdfs:domain`, `rdfs:range`, `rdfs:subClassOf`, and `rdfs:label`, the rules and labels attached to our drawers.

Now extend the model you built with `rdf:type` in *Type your resources*, using RDF Schema.

1. Pick one property that connects two of your resources, for example the relationship between an artwork and its creator. Give it a name, e.g. `ex:createdBy`.
2. Use `rdfs:domain` and `rdfs:range` to state which class of resource can be the subject and which can be the object of that property.
3. If you have two related classes (e.g. `ex:Print` and `ex:Artwork`), connect them with `rdfs:subClassOf`.
4. Add an `rdfs:label` to at least one class or property, so it has a human-readable name.

::: solution

```text
ex:createdBy rdfs:domain ex:Artwork
ex:createdBy rdfs:range ex:Person

ex:Print rdfs:subClassOf ex:Artwork

ex:Artwork rdfs:label "Artwork"
```

With these additional statements we are no longer only listing individual facts, as we did with `rdf:type`. We are now describing rules about how our drawers and connectors relate to each other - what plain RDF alone could not do. This is exactly the purpose of RDF Schema: it lets us describe the *shape* of our data, not just individual data points.

:::
::::

## Vocabularies and Ontologies

So far we have been inventing our own terms, such as `ex:Artwork` or `ex:createdBy`. This is fine for practicing, but it creates a problem: if every project invents its own classes and properties, we cannot easily tell that two datasets are talking about the same kind of thing. Imagine two museums publishing data about their collections. One uses `ex:createdBy`, the other uses `museum:artist`. A computer reading both datasets has no way of knowing that these two properties mean the same thing, unless both museums agree to use the same, shared term.

This is exactly what **vocabularies** and **ontologies** provide: a shared set of classes and properties, each with its own carefully chosen, permanent IRI, that anyone can reuse instead of inventing their own.

- A **vocabulary** is usually a lightweight set of terms, with a short description of what each one means.
- An **ontology** is a more formal, detailed vocabulary that also defines rules and relationships between its terms, for example that "print" is always a subclass of "artwork".

In practice, the two words are often used interchangeably, and the boundary between them is not always sharp.

Some vocabularies and ontologies frequently used in cultural heritage and the humanities:

- [Dublin Core (dc/dcterms)](https://www.dublincore.org/specifications/dublin-core/dcmi-terms/) - general-purpose terms such as `dc:creator`, `dc:title`, or `dc:date`.
- [schema.org](https://schema.org) - a broad vocabulary with terms for people, places, and creative works.
- [FOAF (Friend of a Friend)](http://xmlns.com/foaf/spec/) - describes people, e.g. `foaf:Person`, `foaf:name`.
- [CIDOC CRM](https://www.cidoc-crm.org/) - a detailed ontology for describing museum and cultural heritage information.
- [SKOS](https://www.w3.org/2004/02/skos/) - a vocabulary for thesauri and classification systems.

You rarely need to memorise these. Tools such as [Linked Open Vocabularies (LOV)](https://lov.linkeddata.es/dataset/lov/) or [prefix.cc](https://prefix.cc/) let you search for existing, reusable terms instead of inventing your own.

:::: challenge
## A first look at reusing a vocabulary

Go back to the small model you built with your own `ex:` terms in the previous challenges.

1. Search FOAF or Dublin Core for a term that could replace one of your `ex:` classes or properties, for example a class for "person" or a property for "creator".
2. Rewrite one of your triples using the term you found instead of your own `ex:` term.

::: solution

For our example object `693151`, `ex:SurugueLouis rdf:type ex:Person` could become `ex:SurugueLouis rdf:type foaf:Person`, and `ex:ObjectID693151 hasCreator ex:SurugueLouis` could become `ex:ObjectID693151 dc:creator ex:SurugueLouis`.

Not every term has a good match: none of these general vocabularies has an exact term for "artwork" in a museum context, this is where a more specialised ontology such as CIDOC CRM would come in. It is common, and completely fine, for a real data model to combine several existing vocabularies with a few custom terms for anything specific to the dataset.

:::
::::

Vocabularies like these standardise shared *classes and properties* - the general shape of a description. There is a related but different idea: standardising identifiers for *individual, real-world entities* - a specific person, place, or organisation - so that the same entity is recognised across many datasets, not just the same kind of entity. We will explore this idea, and put it to practical use, when we reconcile our dataset against authority files such as Wikidata in a later chapter.

::: keypoints
- A data model describes which entities exist in a dataset, how they relate, and how they should be described, before creating RDF.
- Resources are identifiable things; literals are plain values; classes describe categories that resources belong to.
- `rdf:type` links a resource to the class it belongs to.
- RDF Schema (RDFS) adds vocabulary for describing data models, e.g. `rdfs:domain`, `rdfs:range`, `rdfs:subClassOf`, and `rdfs:label`.
- Vocabularies and ontologies provide shared, reusable terms so that data models from different projects can be understood by machines and combined with each other.
- Reusing existing vocabularies (e.g. Dublin Core, FOAF, schema.org, CIDOC CRM) instead of inventing new terms improves interoperability.
- Vocabularies standardise shared classes and properties; authority files do the same for individual, real-world entities, this is what reconciliation, covered in a later chapter, connects our model to.
:::
