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

Now, with these IDs, it becomes possible to refer to one exact painting and be sure that everyone within the same context understands which artwork is meant. However, when we are only talking about an ID—a number—it is conceivable that in another context the same number might refer to a different object, meaning that the number alone is not free from ambiguity, so we need to find a way to resolve to that exact "context".

To resolve this problem, we can use a **URI**, a **Uniform Resource Identifier**. By combining a unique ID with a well-defined namespace, a URI guarantees global uniqueness. The namespace acts like a contextual “container” that ensures the ID is interpreted in a specific environment, making it unambiguous no matter where or when it is used. Similarly, **IRIs** extend this principle by allowing a broader set of characters, accommodating diverse languages and scripts. Together, the use of namespaces and IDs ensures that every resource is uniquely identifiable at all times and in every context. The namespace is the "context" mentioned before.


## Understanding IRIs


Applied to the painting *Wheatfield with Cypresses*, the Metropolitan Museum of Art does not provide a guaranteed way to reference this so-called resource unambiguously. While we can use the link to the museum’s website, there is no guarantee that this link will remain unchanged over time. If the URL were to change, our reference would no longer work.  

To avoid this problem, certain providers offer ways to generate IRIs. One example we want to examine is *Wikidata*, the structured data repository behind Wikipedia. If we search for *Wheatfield with Cypresses* on Wikidata, we also find multiple entries. Looking at this [entry](https://www.wikidata.org/wiki/Q26221215), we can already see the associated ID in the page title. The link to the page _https://www.wikidata.org/wiki/Q26221215_ forms the IRI. The first part, _https://www.wikidata.org/wiki/_, is the **namespace**, which is predefined, while the second part, _Q26221215_, is the **ID**, which is uniquely referable within this namespace. The combination of both elements ensures that this object can be referenced unambiguously in different contexts. Like subjects, predicates need to get a IRI aswell, which describes what the predicate means exactly. Wikidata also provides some properties in their [List of Properties](https://www.wikidata.org/wiki/Wikidata:List_of_properties). For example we can find an IRI for the property [place of birth](https://www.wikidata.org/wiki/Property:P19).







## Conclusion

URIs and IRIs form the bedrock of Linked Open Data by ensuring that every digital resource, such as Van Gogh’s *Wheatfield with Cypresses*, has a unique, reliable address. By breaking down the structure of these identifiers and understanding the role of namespaces, we see how ambiguity is resolved. This system not only enhances clarity but also fosters global collaboration and deeper insights in research.





