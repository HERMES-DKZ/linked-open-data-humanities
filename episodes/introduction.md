---
title: "Introduction to Linked Open Data in the Humanities"
teaching: 20
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is Linked Open Data, and how does it differ from other data models?
- Why are standardized identifiers (e.g., URIs) essential for LOD?
- What is the subject-predicate-object model?
- How can the subject-predicate-object model be used to describe LOD?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain the concept of Linked Open Data (LOD).
- Differentiate between 'Linked Data' and 'Linked Open Data'.
- Describe the importance of standardized identifiers (e.g., URIs) for data linking.
- Create Linked Open Data relationships using the subject-predicate-object model.

::::::::::::::::::::::::::::::::::::::::::::::::



## Introduction

In this episode we want to understand the basics of **Linked Open Data**. What is this and why should I use it? To do this, we will split the term **Linked Open Data**, because the first thing we need to understand is: What kind of data we are talking about?


Imagine you are a researcher studying **Vincent van Gogh** and you want to build a collection about this person with, for example, paintings, friends, visited places and so on. Best case scenario would be, if you could use data from other researchers as well to connect the knowledge you collected.

One way to express these knowledge is by breaking it down into relationships using a **subject-predicate-object structure:

- **Subject**: The entity being described.
- **Predicate**: The relationship or property.
- **Object**: The value or linked entity.

But what does this mean in the case of a person? One example would be, if you want to express that the picture "Bouqet of Sunflowers" were painted by Vincent van Gogh.

### Example triple for Van Gogh's painting:
| Subject | Predicate | Object |
|---------|----------|--------|
| "Wheat Field with Cypresses" | was painted by | "Vincent van Gogh" |
| "Wheat Field with Cypresses" | was created in | "1889" |
| "Wheat Field with Cypresses" | is located at | "Metropolitan Museum of Art" |

By structuring data in this way, we make information clearer and easier to connect with other datasets. 

## The Challenge: Ambiguity in Art Titles

Now, let’s say you look up *Wheat Field with Cypresses* in different museum databases and find multiple records:

1. An entry titled *Wheat Field with Cypresses*, attributed to **Vincent van Gogh**, painted in **1889**.
2. Another entry with the same title, attributed to **Vincent van Gogh**, also from **1889**.
3. A third entry under the title *Champ de blé aux cyprès*, again by **Vincent van Gogh**.

Are these all the same painting, or are there multiple versions? Museum records might not provide enough information to clarify this. **How can we ensure that different databases refer to the exact same painting?**

## How URIs Solve Ambiguity

A **Uniform Resource Identifier (URI)** provides a unique reference for an entity, ensuring clarity in data relationships. Instead of relying on titles, which may be duplicated across datasets, we use a globally unique identifier.

For example:
- **Van Gogh's Wheat Field with Cypresses (Metropolitan Museum of Art)**: `https://www.metmuseum.org/art/collection/search/436535`
- **Van Gogh's Wheat Field with Cypresses (Wikidata)**: `https://www.wikidata.org/entity/Q201852`

By linking datasets using these URIs, we can ensure that different records actually refer to the same artwork.

## What is Linked Open Data (LOD)?

Linked Open Data (LOD) is a method of structuring and publishing data in a way that enables connections between different datasets. By following the principles of Linked Data and ensuring open access, LOD allows for seamless data integration across various domains.

Tim Berners-Lee, the inventor of the World Wide Web, outlined **four principles** for Linked Data:

4. **Use URIs** to uniquely identify resources.
5. **Use HTTP URIs** so that resources can be looked up online.
6. **Provide structured and useful information** using standard formats.
7. **Include links to other relevant data** to establish relationships between datasets.

## Real-world examples of Linked Open Data in the humanities

LOD is already being used in humanities research to resolve ambiguity and connect data. Some notable examples include:

- **Wikidata** – A collaborative knowledge base using LOD principles to interconnect historical and biographical data.
- **Europeana** – A digital archive linking cultural heritage collections across Europe, making historical records more accessible.
- **The Met's Linked Open Data Initiative** – A project providing LOD access to its art collection to facilitate data integration and research.

## Exercise: Identifying Ambiguous Art Data

### Task:
Consider the following museum record:

> "The Mona Lisa was painted by Leonardo da Vinci."

8. Identify possible ambiguities in this statement (e.g., which Mona Lisa? Which Leonardo da Vinci?).
9. Find the correct URI for **The Mona Lisa** on **Wikidata**.
10. Express the information as a **subject-predicate-object** triple.

## Summary

- **The subject-predicate-object model structures information clearly, helping to describe relationships.**
- **Ambiguity in data arises when different records use similar names without unique identifiers.**
- **URIs solve this issue by providing a single reference point for entities.**
- **Linked Open Data connects different datasets, allowing for richer, more accurate research.**

In the next lesson, we will explore **how Linked Data can be used to build complex relationships between datasets.**
