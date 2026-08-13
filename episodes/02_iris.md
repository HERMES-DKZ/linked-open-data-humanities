---
title: "The concept of IRIs"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions

- How do IRIs eliminate ambiguity when different datasets use similar titles?
- What are the essential components of a IRI, and how do they work together to ensure uniqueness?
- Why are namespaces crucial for maintaining clarity and consistency in linked data?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain what IRIs are 
- Explain why they are important in Linked Open Data.
- Explain the structure of a IRI
- Explain what namespaces are

::::::::::::::::::::::::::::::::::::::::::::::::


## Ambiguity  

Now that the fundamental concept behind the subject-predicate-object model is understood, a problem arises when trying to connect your own data with external datasets or when modeling knowledge unambiguously: How can we ensure that we are talking about the same objects?  

Consider the following example:  

Suppose you are researching in the database from the [Metropolitan Museum of Art](https://www.metmuseum.org/art/collection) for Van Gogh’s painting _Wheat Field with Cypresses_. Now, if you would like to talk about the different paintings, it could become difficult and confusing which painting you want to talk about exactly, because you find:  

1. An entry titled *Wheatfield with Cypresses*, attributed to **Vincent van Gogh**, painted in **1889**.  

2. Another entry titled *Cypresses*, also attributed to **Vincent van Gogh**, from **1889**.  

3. Another entry titled *Wheat Field*, also by **Vincent van Gogh** from **1888**.  

4. Yet another entry with the same title *Wheat Field*, but by **Jean Jacques de Boissieu** from **1772**.  

This highlights that names are often not unique. While additional details like year and artist usually clarify which object is meant, this is not always guaranteed. Humans can often resolve such ambiguities using context, but computers struggle with this.  

Since a subject-predicate-object model does not have the context of a larger text, ambiguity can be resolved using IDs. Museums, for instance, assign unique IDs to paintings, ensuring that even those with identical names are distinguishable. This concept is adapted and expanded for LOD to work in an open, large-scale environment.

Now, with these IDs, it becomes possible to refer to one exact painting and be sure that everyone within the same context understands which artwork is meant. However, when we are only talking about an ID, a number, it is conceivable that in another context the same number might refer to a different object, meaning that the number alone is not free from ambiguity, so we need to find a way to resolve to that exact "context".

## From IDs to URIs

To resolve this problem, we can use a **URI**, a **Uniform Resource Identifier**. The key idea is to combine a unique ID with a **namespace** and together they form a globally unique address.

Think of it like a postal address. If someone tells you “the house is number 42”, that is not very helpful, there are thousands of houses numbered 42 in the world. But “42 Baker Street, London” is unambiguous. The house number is the **ID**, and the street and city together form the **namespace**: they provide the context that makes the number meaningful.

Back to our example: the Metropolitan Museum of Art assigns the internal ID `436535` to *Wheatfield with Cypresses*. Another museum might use the very same number for a completely different object. But by combining that ID with the name of the institution as the **namespace**, the combination `Metropolitan Museum of Art / 436535` is already unambiguous. The namespace is therefore not just a technical prefix, it is a declaration of context: *”this ID belongs to this institution, and has a defined meaning there”*.

In Linked Open Data, this principle is taken a step further: namespaces are defined as addresses on the internet, so that every resource can be looked up and referenced globally by anyone. This turns a namespace-and-ID combination into a **URI** (Uniform Resource Identifier), a unique, web-resolvable address. **IRIs** (Internationalized Resource Identifiers) extend this further by also supporting non-Latin scripts such as Arabic, Chinese, or Japanese.

:::::::::::::::::::::::::::::::::::::: callout

### URI and IRI in a nutshell

A **URI** is a unique, web-resolvable address for an object, made up of two parts:

- The **namespace** gives the context, a web address identifying the institution or system that manages the data
- The **ID** identifies the specific object within that context

Together: `namespace` + `ID` = URI, a globally unique address that anyone can look up.

An **IRI** works exactly the same way, but also supports non-Latin characters.

::::::::::::::::::::::::::::::::::::::::::::::


## Understanding IRIs


Applied to the painting *Wheatfield with Cypresses*, the Metropolitan Museum of Art does not provide a guaranteed way to reference this so-called resource unambiguously. While we can use the link to the museum’s website, there is no guarantee that this link will remain unchanged over time. If the URL were to change, our reference would no longer work.  

To avoid this problem, certain providers offer ways to generate IRIs. One example we want to examine is *Wikidata*, the structured data repository behind Wikipedia. If we search for *Wheatfield with Cypresses* on Wikidata, we also find multiple entries. Looking at this [entry](https://www.wikidata.org/wiki/Q26221215), we can already see the associated ID in the page title. The link to the page _https://www.wikidata.org/wiki/Q26221215_ forms the IRI. The first part, _https://www.wikidata.org/wiki/_, is the **namespace**, which is predefined, while the second part, _Q26221215_, is the **ID**, which is uniquely referable within this namespace. The combination of both elements ensures that this object can be referenced unambiguously in different contexts. Like subjects, predicates need to get a IRI aswell, which describes what the predicate means exactly. Wikidata also provides some properties in their [List of Properties](https://www.wikidata.org/wiki/Wikidata:List_of_properties). For example we can find an IRI for the property [place of birth](https://www.wikidata.org/wiki/Property:P19).




## Exercise

:::::::::::::::::::::::::::::::::::::: challenge

## One Entity, Two IRIs

In LOD, the goal is to identify every resource unambiguously. But what happens when different systems each assign their own IRI to the same entity?

1. Open [Wikidata](https://www.wikidata.org) and find the entry for **Vincent van Gogh**. Note down his IRI.
2. Now open [VIAF](https://viaf.org) (Virtual International Authority File) and search for Vincent van Gogh. Note down his IRI there as well.
3. Identify the **namespace** and the **ID** in each IRI.
4. You now have two different IRIs for the same person. Does this contradict the LOD principle of unambiguous identification? Look carefully at the Wikidata entry for Van Gogh. Can you find anything that addresses this problem?

:::::::::::::::: solution

**Wikidata IRI**: `https://www.wikidata.org/wiki/Q5582`
Namespace: `https://www.wikidata.org/wiki/` — ID: `Q5582`

**VIAF IRI**: `https://viaf.org/viaf/9854560`
Namespace: `https://viaf.org/viaf/` — ID: `9854560`

Both IRIs are internally unambiguous. Within their own system, each points to exactly one entity. The apparent contradiction is resolved by the fact that LOD systems can explicitly declare that two IRIs refer to the same thing. In the Wikidata entry for Van Gogh, you can find the property **VIAF ID** with the value `9854560` , a direct link to the VIAF record. The two systems are already connected.

This is a fundamental pattern in LOD: rather than forcing a single global ID on every entity, different institutions maintain their own IRIs and link them to each other. How exactly this linking works will be covered in a later chapter.

:::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::::::::::::::::


## Conclusion

URIs and IRIs form the bedrock of Linked Open Data by ensuring that every digital resource, such as Van Gogh’s *Wheatfield with Cypresses*, has a unique, reliable address. By breaking down the structure of these identifiers and understanding the role of namespaces, we see how ambiguity is resolved. This system not only enhances clarity but also fosters global collaboration and deeper insights in research.

:::::::::::::::::::::::::::::::::::::: keypoints

- IRIs (Internationalized Resource Identifiers) are used to prevent ambiguities when identifying resources.
- An IRI needs to be defined and resolvable on the web.
- Subjects, predicates, and non-literal objects are identified with IRIs.
- An IRI is created from a namespace in combination with an ID.

::::::::::::::::::::::::::::::::::::::::::::::::::
