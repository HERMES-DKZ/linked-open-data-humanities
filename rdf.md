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


## Introduction

In the previous lesson, we explored the fundamentals of **Linked Open Data (LOD)** and how information can be structured using the **subject-predicate-object** model. We learned how using **URIs** helps to uniquely identify entities, avoiding ambiguity in datasets.  

In this episode, we will go a step further and introduce the **Resource Description Framework (RDF)**. RDF is the standard model used to structure Linked Open Data, allowing us to represent knowledge in a machine-readable way.  


---

## What is RDF and Why Do We Need It?

The **Resource Description Framework (RDF)** is a framework for representing structured data on the web. It provides a **universal way to describe relationships between entities**, making it easier to link and integrate different datasets.  

But why do we need RDF? Let's consider an example:

Imagine you are researching **Leonardo da Vinci** and his works. You visit different online databases and find information about his paintings, inventions, and biography. However, each database structures its information differently:
- One website lists his paintings in a simple table.
- Another site describes his life in paragraphs of text.
- A third database provides numerical IDs for each artwork but no additional links.

Since each database uses a **different format**, it becomes difficult to combine and compare data. **RDF solves this problem** by providing a structured format that allows computers to understand and process relationships between entities. This means:
- Data from different sources can be easily combined.
- Relationships between entities become explicit.
- Machines (and humans) can navigate and query data efficiently.

To achieve this, RDF follows a simple but powerful structure: the **triple model**.

---

## RDF and the Triple Model

RDF represents data using **triples**, which follow the **subject-predicate-object** pattern we introduced in the previous lesson. This structure allows us to describe relationships between things in a clear and machine-readable way.  

Each RDF triple consists of three components:

1. **Subject**: The entity being described (e.g., a person, a painting, a place).
2. **Predicate**: The property or relationship connecting the subject and object.
3. **Object**: The value or linked entity.

Let's look at an example in the context of art history.

### Example: Describing a Painting in RDF

Suppose we want to describe the fact that **Leonardo da Vinci painted the Mona Lisa**. We can structure this as subject-predicate-object relationships:

| Subject | Predicate | Object |
|---------|----------|--------|
| `Mona Lisa` | `was painted by` | `Leonardo da Vinci` |

In RDF, we typically use **URIs** instead of plain text labels to uniquely identify resources. This avoids confusion between similar names (e.g., different artworks named "Mona Lisa" or multiple people named "Leonardo da Vinci").  

Here is how the same fact would be expressed using URIs:

| Subject | Predicate | Object |
|---------|----------|--------|
| `<https://www.wikidata.org/entity/Q12418>` | `<https://schema.org/creator>` | `<https://www.wikidata.org/entity/Q762>` |

- `<https://www.wikidata.org/entity/Q12418>` → The URI for the **Mona Lisa**.
- `<https://schema.org/creator>` → A standard property for describing the **creator of an artwork**.
- `<https://www.wikidata.org/entity/Q762>` → The URI for **Leonardo da Vinci**.

By using **URIs**, we ensure that the data is clear and unambiguous. Any database referencing these URIs will automatically refer to the same entities, making it easy to merge and connect data.

---

## Modeling Real-World Relationships with RDF

RDF allows us to represent **complex knowledge networks** by linking multiple pieces of information. Let's extend our example and describe more facts about Leonardo da Vinci.

| Subject | Predicate | Object |
|---------|----------|--------|
| `<https://www.wikidata.org/entity/Q12418>` | `<https://schema.org/creator>` | `<https://www.wikidata.org/entity/Q762>` |
| `<https://www.wikidata.org/entity/Q762>` | `<https://schema.org/birthPlace>` | `<https://www.wikidata.org/entity/Q2044>` |
| `<https://www.wikidata.org/entity/Q762>` | `<https://schema.org/occupation>` | `Painter` |

This data tells us:
1. **Leonardo da Vinci created the Mona Lisa**.
2. **Leonardo da Vinci was born in Vinci, Italy**.
3. **Leonardo da Vinci’s occupation was "Painter"**.

By structuring data in this way, we create **a network of linked facts** that can be queried, analyzed, and combined with other datasets.

---

## Exercise: Representing RDF Triples

### Task 1: Identifying Triples in a Sentence

Consider the sentence:  
> "Vincent van Gogh painted Starry Night in 1889."

1. Identify the **subject**, **predicate**, and **object** in this statement.
2. Represent the information in a structured table.
3. Try to express the same fact using **URIs**.

### Task 2: Expanding the RDF Graph

Based on the example above, add **two additional pieces of information** about Vincent van Gogh to the dataset.  
For example:
- Where was he born?
- What kind of artist was he?

Write down your new RDF triples in a table format.

---

## Limitations of RDF

While RDF is a powerful tool for structuring Linked Open Data, it also has some limitations:

1. **Data Complexity**  
   RDF models can become very large and complex, especially when dealing with vast datasets. Querying and managing large RDF graphs requires specialized tools.

2. **Understanding and Adoption**  
   Since RDF requires a structured approach and the use of URIs, it can be challenging for beginners and institutions unfamiliar with semantic web technologies.

3. **Data Linking Challenges**  
   Although RDF enables linking data across sources, ensuring **consistent and high-quality links** requires effort and collaboration between organizations.

Despite these challenges, RDF remains a **key technology for Linked Open Data**, enabling the creation of rich, connected knowledge graphs.

---


