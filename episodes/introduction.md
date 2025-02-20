---
title: "Introduction to Linked Open Data in the Humanities"
teaching: 20
exercises: 10
---

## Introduction

In this lesson, we want to explore the basics of **Linked Open Data (LOD)**. What is it, and why is it important? To answer these questions, we will break down the term step by step. The first and most fundamental thing we need to understand is: **What kind of data are we dealing with?**

Imagine you are a researcher studying **Vincent van Gogh**, and you want to build a collection of information about him. You might collect details about his paintings, his friends, the places he visited, and much more. The best-case scenario would be if you could **connect** your collected knowledge with data from other researchers. But how can we structure this knowledge in a way that makes it easy to share, connect, and expand?

### Structuring Knowledge: The Subject-Predicate-Object Model

A powerful way to structure and connect knowledge is by breaking it down into **simple relationships** using the **subject-predicate-object** model. This model is a fundamental way of expressing data in a structured format:

- **Subject**: The entity being described.
- **Predicate**: The relationship or property.
- **Object**: The value or linked entity.

For example, if we want to express that Vincent van Gogh painted *Bouquet of Sunflowers*, we can structure it like this:

#### Example Triple for Van Gogh's Painting
| Subject | Predicate | Object |
|---------|----------|--------|
| *Bouquet of Sunflowers* | was painted by | *Vincent van Gogh* |

By structuring data in this way, we make information **clearer, more precise, and easier to connect with other datasets**.

### Creating a Simple Mindmap

To visualize how Linked Open Data works, let's think about a **mindmap**. Imagine writing *Vincent van Gogh* at the center of a page. Now, draw lines to different connected terms:

- One line connects to *Bouquet of Sunflowers* with the label **was painted by**.
- Another line connects to *Zundert* (his birthplace) with the label **was born in**.
- A third line connects *Zundert* to *Netherlands* with the label **is part of**.

Each of these connections expands the **network of knowledge**—a simple version of what we call the **LOD cloud**. The more links we create, the richer and more meaningful our dataset becomes. 

---

## The Challenge: Ambiguity in Art Titles

Now, let’s say you are researching Van Gogh’s painting *Wheat Field with Cypresses* and you check multiple museum databases. You find several records:

1. An entry titled *Wheat Field with Cypresses*, attributed to **Vincent van Gogh**, painted in **1889**.
2. Another entry with the same title, also attributed to **Vincent van Gogh**, also from **1889**.
3. A third entry under the French title *Champ de blé aux cyprès*, again by **Vincent van Gogh**.

Are these all referring to the same painting, or are there multiple versions? Museum records might not provide enough information to clarify this. **How can we ensure that different databases refer to the exact same artwork?**

---

## How URIs Solve Ambiguity

A **Uniform Resource Identifier (URI)** provides a unique reference for an entity, ensuring clarity in data relationships. Instead of relying on **titles**, which might be duplicated across datasets, we use a **globally unique identifier**.

For example:
- **Van Gogh's Wheat Field with Cypresses (Metropolitan Museum of Art)**: `https://www.metmuseum.org/art/collection/search/436535`
- **Van Gogh's Wheat Field with Cypresses (Wikidata)**: `https://www.wikidata.org/entity/Q201852`

By linking datasets using these **URIs**, we can ensure that different records actually refer to the **same artwork**.

---

## What is Linked Open Data (LOD)?

**Linked Open Data (LOD)** is a way of **structuring and publishing data** that enables connections between different datasets. By following the principles of **Linked Data** and ensuring **open access**, LOD allows for **seamless data integration across various domains**.

Tim Berners-Lee, the inventor of the **World Wide Web**, outlined **four key principles** for Linked Data:

1. **Use URIs** to uniquely identify resources.
2. **Use HTTP URIs** so that resources can be looked up online.
3. **Provide structured and useful information** using standard formats.
4. **Include links to other relevant data** to establish relationships between datasets.

When we follow these principles, we create **interconnected datasets** that can be used, combined, and enriched by anyone in the world.

---

## Real-World Examples of Linked Open Data in the Humanities

LOD is already widely used in **humanities research** to **resolve ambiguity** and **connect data** across institutions. Some notable examples include:

- **Wikidata** – A collaborative knowledge base that uses LOD principles to interconnect historical and biographical data.
- **Europeana** – A digital archive linking cultural heritage collections across Europe, making historical records more accessible.
- **The Met's Linked Open Data Initiative** – A project providing LOD access to its art collection, allowing researchers to integrate data more effectively.

These projects **enhance accessibility, improve research quality, and allow datasets to grow beyond the limits of individual institutions**.

---

## Exercise: Identifying Ambiguous Art Data

### Task:
Consider the following museum record:

> "The Mona Lisa was painted by Leonardo da Vinci."

1. Identify possible **ambiguities** in this statement (e.g., **which** Mona Lisa? **Which** Leonardo da Vinci?).
2. Find the correct **URI** for **The Mona Lisa** on **Wikidata**.
3. Express the information as a **subject-predicate-object** triple.
4. Create a **simple mindmap** connecting *Leonardo da Vinci* with his paintings, birthplace, and other notable facts.

---

## Summary

- **The subject-predicate-object model structures information clearly, helping to describe relationships between entities.**
- **Ambiguity in data arises when different records use similar names without unique identifiers.**
- **URIs solve this issue by providing a single reference point for each entity.**
- **Linked Open Data connects different datasets, allowing for richer, more accurate research.**

In the next lesson, we will explore **how RDF (Resource Description Framework) formalizes this model and enables structured data exchange.**
