---
title: "Introduction to Linked Open Data in the Humanities"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is Linked Open Data, and how does it differ from other data models?
- Why are standardized identifiers (e.g., URIs) essential for LOD?
- How can the subject-predicate-object model be used to describe LOD?
- What are real-world examples of Linked Open Data in the humanities?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain the concept of Linked Open Data (LOD) in your own words.
- Distinguish between "Linked Data" and "Linked Open Data".
- Describe the importance of standardized identifiers (e.g., URIs) for linking data.
- Represent simple relationships using the subject-predicate-object model.

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

In this lesson, we want to explore the fundamentals of **Linked Open Data (LOD)**. What is it, and why is it important? To answer these questions, we will break the term down step by step. The first and most fundamental concept we need to understand is: **What type of data are we dealing with? In what form does data exist when we talk about LOD?**  To do this, first we want to look at the terms *linked*, *open*, and *data*, to understand what we are talking about in the first place.

:::::::::::::::::::::::::::::::::::::: discussion

### Discussion: What is data? 

When we talk about data, many people often understand different things about it, and no-one can quite put their finger on what it actually means. Try to approach this term and find out what it could mean. 

::::::::::::::::::::::::::::::::::::::::::::::::::


It is not easy to find a universal definition of data, but a useful starting point is: **data is information about the real world that has been observed and recorded**. Think of it like a photograph. A photo captures a moment in time, but it can never show everything: the smell in the air, the sounds in the background, or what happened the moment before. Data works the same way.

In the humanities, data can take many forms:

- A **letter** written by a historical figure is data. It records words, a date, a sender, and a recipient.
- An **archaeological object**, such as a Roman coin, is data. It records material, size, imagery, and findspot.
- A **painting** like the *Starry Night* is data. It records a creative act at a specific time and place.

In the natural sciences, data is often a number: the temperature on a given day or the weight of a sample. What all of these have in common is that they try to **represent a portion of the real world**.

This also means that data is always **incomplete and selective**. It is impossible to capture everything about a Roman coin just by noting its diameter. Someone, a researcher, a curator, a museum, has to decide which properties are worth recording and which are not. These decisions are always tied to a specific purpose and perspective, and they shape what the data can and cannot tell us.

In our digital age, much of this data exists or is being transferred into digital form. This makes it easier to store, share, and analyse, but it also intensifies these challenges: **what we digitise, and how we digitise it, determines what future researchers will be able to find and understand.**

Now that we understand what data is, we want to look at how it can be captured and digitised, which is why we will look at the L from LOD next.


:::::::::::::::::::::::::::::::::::::: discussion

### Discussion: What requirements should data fulfil?

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::: discussion

### Discussion: What data modelling options do you know?

::::::::::::::::::::::::::::::::::::::::::::::::::


Imagine you are a researcher studying **Vincent van Gogh** and want to build a collection of information about him. You could gather details about his paintings, his friends, the places he visited, and much more. Probably the most common way would be to store this information in a table. This has various advantages, but also disadvantages. As with the collection of data and writing it down, there is no clear answer as to which type of modelling is correct, it remains individual and above all depends on the project. If you want to combine your own data with other data, such as information about Van Gogh's home town or his circle of acquaintances, it becomes difficult to visualise this in a table. The question is now, how we structure our knowledge in a way, that is easy to share, connect, and expand?  



## Structuring Knowledge: The Subject-Predicate-Object Model  

Given the following Information about **Vincent Van Gogh**: He was **born** in **Zundert** and has **drawn** the painting **Starry Night**

One way to structure and link knowledge is to break it down into **simple relationships** using the **subject-predicate-object** model. This model is a fundamental method for structured data representation:  


:::::::::::::::::::::::::::::::::::::: callout

### The subject-predicate-object model

**Subject**: The entity being described.  

**Predicate**: The relationship or attribute.  

**Object**: The value or linked entity. 

::::::::::::::::::::::::::::::::::::::::::::::::::


For example, if we want to express that Vincent van Gogh painted *Starry Night*, we can structure it like this:  


| Subject                 | Predicate      | Object             |
| ----------------------- | -------------- | ------------------ |
| *Bouquet of Sunflowers* | was painted by | *Vincent van Gogh* |


By structuring information in this way, we ensure that the knowledge we store—namely, that Vincent van Gogh painted this artwork—is precise and easy to understand. We reduce the sentence to the essential elements, making it easier to store and process.  

Now, if we wanted to store additional paintings by Vincent van Gogh, we could use the same format. Adding another painting to the table would look like this:  


| Subject                 | Predicate      | Object             |
| ----------------------- | -------------- | ------------------ |
| *Bouquet of Sunflowers* | was painted by | *Vincent van Gogh* |
| *Starry Night*          | was painted by | *Vincent van Gogh* |



However, at this point, our data is still in a tabular format, which is not the format used in LOD.  


## Triples Visualized

To visualize how Linked Open Data works, imagine a **mind map**. Write *Vincent van Gogh* in the center of a page and draw lines to various related terms:  

- One line connects *Bouquet of Sunflowers* with the label **was painted by**.  

- Another line connects *Zundert* (his birthplace) with the label **was born in**.  

- A third line connects *Zundert* with *Netherlands* with the label **is part of**.  

Each of these connections expands the **knowledge network**—a simple version of what we call the **LOD cloud**. The more connections we create, the richer and more meaningful our dataset becomes. The resulting mind map would look like this:  


![](fig/mind_map_example.png)


By visualizing the data, it becomes easier to see why this way of storing and structuring knowledge is so efficient and valuable. Imagine a much larger mind map with significantly more information. This could reveal connections between people that were previously invisible. Furthermore, if researchers from different locations collaborate on such a mind map, additional insights and knowledge can be discovered. In a very theorital and ideal scenario it would be possible to draw a mindmap with every information in the world to find a connection from you to Bill Gates.

In essence, we are working with graphs, more specifically, directed graphs that follow a particular reading direction. Each connection has a clear subject, predicate, and object, forming what’s known as a triple. 

:::::::::::::::::::::::::::::::::::::: challenge  

## Exercise: Create a Graph  

Look at one of the following texts and try to visualise the information from it in a mind map. Pay attention to decisions that need to be made and possible problems that may arise. To draw the mind map you can use whatever you want. One possibility is [Excalidraw](https://excalidraw.com/) , an open source tool with which you can also work in a group
Go into breakout rooms and create a graph. Try to find connections you could model in that graph.  

---

**Group 1**: Vincent van Gogh was born in Zundert, the Netherlands, in 1853 and is a Post-Impressionist artist. In his youth, he developed a strong interest in art and initially studied in The Hague. He later moved to Paris, where he gained his first insights into modern art.

---

**Group 2**: Van Gogh created numerous famous paintings. The masterpiece ‘Starry Night’ was created in Saint-Remy-de-Provence and belongs to the Post-Impressionist era. The painting can be found in the Museum of Modern Art in Manhattan.

:::::::::::::::: solution

One way to visualize both texts in one graph is the following. If your solution looks different, this does not necessarily mean that it is wrong. It is, as always in data modelling, individual and decision based.

![](fig/solution_mind_map.png)

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::  





