---
title: "Reconciliation"
teaching: 30
exercises: 1
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is reconciliation and why does it matter for Linked Data?
- How do authority files relate to the vocabularies and ontologies we reused earlier?
- How do I reconcile a column against Wikidata in OpenRefine?
- How do I use reconciled values to add authority IRIs to my RDF mapping?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain what reconciliation is and why it is a key step in creating Linked Open Data.
- Explain how authority files relate to the vocabularies and ontologies introduced earlier.
- Reconcile columns against Wikidata in OpenRefine.
- Review, accept, and reject candidate matches.
- Add `schema:sameAs` links to the Person entity using the reconciled Wikidata IRIs.

::::::::::::::::::::::::::::::::::::::::::::::::


In the model chapter, we reused vocabularies and ontologies, such as Dublin Core, FOAF, or schema.org, so that our classes and properties would mean the same thing across different projects. That solved the problem of *classes and properties*: two datasets that both use `foaf:Person` clearly mean the same *kind* of thing. It did not yet solve a related problem: knowing that two datasets both describe *a* person does not tell us whether they describe the *same* person.

## From Placeholders to Real Identifiers

In the previous chapter, we created a Person entity for each artist in our dataset. The subject IRI was constructed from the artist's name — `http://example.org/person/Surugue%2C+Louis`. This works within our dataset: the IRI is unique, consistent across rows, and stable enough for the mapping to function.

But it is still a local placeholder. Nothing outside our dataset knows what `http://example.org/person/Surugue%2C+Louis` refers to. It cannot be connected to information about this artist in other datasets, and a system working with Wikidata or any other authority file has no way to recognise it as the same person.

This is the gap between a local RDF dataset and genuine **Linked Open Data**. To close it, we need to connect our local entities to identifiers that the wider LOD ecosystem already knows: identifiers in authority files like Wikidata, ULAN, or the GND.

The process of establishing these connections is called **reconciliation**.


:::::::::::::::::::::::::::::::::::::: callout

### Why Authority Files?

An **authority file** is a curated, maintained list of entities, for example persons, places, organisations, each with a stable identifier and a canonical form of the name. Authority files are maintained by libraries, archives, research institutions, or other communities. They exist precisely to solve the problem of ambiguous or inconsistent names.

That "stable identifier" is exactly the kind of IRI we met earlier: a namespace (e.g. `https://www.wikidata.org/wiki/`) combined with an ID (e.g. `Q5981497`), globally unique and resolvable, so the same entity can be referenced unambiguously from anywhere on the web. An authority file is, in a sense, simply a large, curated collection of such IRIs, one per real-world entity, rather than one per class or property.

You can think of an authority file as a vocabulary too, just of a different kind: instead of standardising what "creator" means, it standardises *who* a specific creator is.

Wikidata is the largest openly accessible authority file and covers an enormous range of entities. **ULAN** (Union List of Artist Names, Getty Research Institute) is a domain-specific authority for artists and architects. Both are widely used in the cultural heritage sector.

When you reconcile against these sources, your data gains a connection to a global knowledge network and any other dataset that has reconciled against the same source is now implicitly connected to yours.

::::::::::::::::::::::::::::::::::::::::::::::::::


### What Is Reconciliation?

Reconciliation means matching the values in a column against the entities in an external authority file and finding the best correspondence for each value.

In practice: you take the text "Surugue, Louis" and ask Wikidata: *is there an entity in your system that matches this name?* Wikidata returns one or more candidates with confidence scores. You review them, confirm the correct match, and the local text value is now linked to a globally recognised IRI: `https://www.wikidata.org/wiki/Q5981497`.

This is not about replacing your local data. The local placeholder IRI remains the subject of your RDF graph. What reconciliation adds is a link to the same entity in another dataset. Any system following that link can retrieve everything the other dataset, in our example Wikidata, knows about the person without you having to include it yourself.


## Reconciling Against Wikidata

OpenRefine has a built-in reconciliation client that can query any reconciliation service endpoint. Wikidata provides one out of the box.

**Start the reconciliation:**

1. Click the dropdown arrow on the `artist` column header in Open Refine, not the RDF-Transform window.
2. Select *Reconcile* → *Start reconciling...*.
3. In the dialog that opens, select **Wikidata (en)** from the list of available services and click **Next**.
4. Under *Reconcile each cell to an entity of type*, type `human` and select the result *human (Q5)*. This tells Wikidata that you are looking for people, which narrows the search and improves match quality.
5. Click *Start reconciling*.

OpenRefine will now query Wikidata for every unique value in the `artist` column. Depending on the number of distinct values and network speed, this may take a moment.

![The Reconcile panel after opening the Reconcilation and setting human from Wikidata](fig/reconciling_empty.png)


### Reviewing Matches

In some cases, Open Refine will be certain that it has selected the correct entity, while in others it will not. In cases where it is certain, the name is displayed directly in blue as a link that takes you to the entry in Wikidata.
In other cases, various entities are displayed from which you must choose. In our case, for example, in row 8. There, OpenRefine is unsure, and we must explicitly confirm once again whether the entity found is the correct one. If we look at the Wikidata entry, we can see that the person listed there was active in Modena, a city that is also found in our data. That is enough for us to be certain in this case. Now we can click the single tick (✓) to confirm the entity or the double tick (✓✓) to perform this action for all fields associated with this entity. In row 10, with Rudolph Ackermann, it gets more difficult. There, we have two people to choose from, and since we have little other information in our dataset, it is difficult to be certain which entity is the correct one. If no candidate is correct, you can leave the cell unmatched, search for a match by hand or even create a new Entity in wikidata. 

:::::::::::::::::::::::::::::::::::::: callout

### Not every match will succeed

For "well-known" artists Wikidata will typically return a confident single match. For "lesser-known", historical, or ambiguously named artists, the match may be uncertain or absent. This is expected. Reconciliation improves data quality where it can; it does not require perfection to be useful. Even a partial reconciliation, covering 60 % of artists, significantly increases the connectedness of the dataset. However, reconciliation always requires expertise and domain knowledge. In our example, it is already clear that some decisions cannot be made without further research.

::::::::::::::::::::::::::::::::::::::::::::::::::


As mentioned earlier, we have only created a link within Open Refine so far. If we want to supplement the underlying data with the new information, we need to add a new column containing that information:

1. Click the dropdown arrow in the `artist` column again
2. **Reconcile** -> **Add column with URLs of matched entities**
3. Enter **artistSameAs** as column name

Now you can see a new column in your data linking the artist to the corresponding Wikidata entity.



## Applying Reconciled IRIs in RDF-Transform

Confirming a match in OpenRefine does not automatically change the exported RDF, we still need to tell RDF-Transform to use the reconciled Wikidata IRI. We do this by adding a `schema:sameAs` property to the Person root node.

Note that `schema:sameAs` is not a new mechanism, it is simply another property from the schema.org vocabulary we already used for `schema:Person` and `schema:description`. Reconciliation does not require its own special vocabulary, it reuses the vocabularies we already know to state one more kind of fact: that two IRIs refer to the same real-world entity.

1. Open the RDF-Transform panel (*RDF Transform* → *Edit RDF Transform...*).
2. Find the Person root node.
3. Add a new property: `schema:sameAs`.
4. Add a new object to this property.
5. Set the Content to our new **artistSameAs** column
4. Sett **Content used... to IRI.

RDF-Transform will now read the reconciled Wikidata IRI for each cell and write it as the value of `schema:sameAs`. Cells that were not reconciled will produce no triple for this property.

Switch to the *Preview* tab to check the result. A successfully reconciled artist should now appear like this:

```turtle
<example.de/Surugue,Louis>
        rdf:type            schema:Person;
        rdfs:label          "Surugue, Louis";
        schema:description  "French, Paris ca. 1686–1762 Grand Vaux";
        schema:sameAs       <https://www.wikidata.org/wiki/Q5981497> .
```

The local IRI remains the subject. The `schema:sameAs` link connects it to the Wikidata entity. Both are now part of the triple, and any system following the `schema:sameAs` link can retrieve the full Wikidata record for this person.



## Going Further: Adding Another Reconciliation Service

In the previous example, we used the built-in Wikidata reconciliation service. However, Wikidata is only one of many authority files that can be used with OpenRefine. Many libraries, museums, and research institutions provide their own reconciliation services. Once a service has been added to OpenRefine, it can be used just like Wikidata.

As an example, we will add another reconciliation service and use it to reconcile the `country` column.

### Step 1: Open the Reconciliation Dialog

1. Click the dropdown arrow of the `country` column.
2. Select **Reconcile → Start reconciling...**

The reconciliation dialog opens. You will see a list of available reconciliation services. Wikidata is already included, but you can also add additional services.

### Step 2: Add a New Reconciliation Service

1. In the reconciliation dialog, click **Add Standard Service...**
2. A new window opens asking for a **Service URL**.
3. If you already know the Service URL, paste it into the input field. If not, click **Cancel** and then **Discover services...** in the reconciliation window.
4. A new window opens showing services supported by OpenRefine. Search for **GeoNames**, copy the Service URL, return to OpenRefine, and click **Add Standard Service...** again.
5. Paste the copied Service URL into the input field.
6. Click **Add Service**.

The new service is now available in the list of reconciliation services. You only need to add it once. It will remain available in future OpenRefine projects.

:::::::::::::::::::::::::::::::::::::: callout

### Common Authority Files in the Digital Humanities

Just like the general-purpose vocabularies we compared in the model chapter (Dublin Core, FOAF, schema.org, CIDOC CRM), authority files differ in scope and level of formality. There is no single authority file that covers every type of entity, so different communities maintain different ones.

Some of the most commonly used authority files in the Digital Humanities include:

| Authority file | Best suited for |
|----------------|-----------------|
| **Wikidata** | General-purpose knowledge graph covering people, places, organisations, events, works, concepts, and many other entity types. |
| **GeoNames** | Geographic entities such as countries, cities, mountains, rivers, and other places. |
| **GND (Integrated Authority File)** | Persons, organisations, places, works, and subjects. Widely used by libraries in German-speaking countries. |
| **Getty ULAN** | Artists, architects, and other creators. Commonly used by museums and art history projects. |
| **Getty AAT** | Concepts such as materials, techniques, object types, styles, and periods. |
| **Getty TGN** | Geographic names and historical places, especially for cultural heritage collections. |
| **VIAF (Virtual International Authority File)** | Links together person and corporate body identifiers from many national libraries worldwide. |

When choosing a reconciliation service, consider which authority file best matches the type of data in your column. For example, **GeoNames** is a good choice for countries and cities, while **ULAN** is better suited for artists and **AAT** for concepts such as materials or object types.

::::::::::::::::::::::::::::::::::::::::::::::::::

### Step 3: Reconcile the Column

1. Select the newly added reconciliation service.
2. Click **Next**.
3. If the service lets you choose an entity type, select the most appropriate one, in our case **Concept**.
4. Click **Start reconciling**.

OpenRefine now compares every unique value in the `country` column with the entries in the selected authority file.

### Step 4: Review the Suggested Matches

As before, OpenRefine proposes one or more possible matches for each value. Review the suggestions carefully before accepting them. It is still your responsibility to decide whether the suggested entity is correct. If you are unsure, it is better to leave a value unreconciled than to create an incorrect link.

### Step 5: Store the Matched Identifiers

After the reconciliation has finished, you can create a new column containing the identifiers of the matched entities.

1. Click the dropdown arrow of the `country` column.
2. Select **Reconcile → Add column with URLs of matched entities**.
3. Name the new column `countrySameAs`.

The new column now contains the authority identifiers returned by the reconciliation service. You can use these identifiers in your RDF mapping in exactly the same way as the `artistSameAs` column created earlier.

:::::::::::::::::::::::::::::::::::::: callout

### Reconciliation Works for Many Types of Data

Reconciliation is not limited to people.

You can reconcile many different kinds of entities, including:

- people
- places
- organisations
- countries
- concepts
- materials
- object types

The workflow is always the same:

1. Choose a column.
2. Select a reconciliation service.
3. Review the suggested matches.
4. Accept the correct matches.
5. Use the resulting identifiers in your RDF mapping.

::::::::::::::::::::::::::::::::::::::::::::::::::

:::::::::::::::::::::::::::::::::::::: challenge

## Exercise: Reconcile the City Column

Repeat the reconciliation workflow using the `city` column.

::::::::::::::::::::::::::::::::::::::::::::::::::


:::::::::::::::::::::::::::::::::::::: keypoints

- Vocabularies and ontologies standardise shared classes and properties; authority files (Wikidata, ULAN, GND, VIAF, GeoNames, ...) standardise identifiers for individual, real-world entities.
- Reconciliation matches a local value against the entities in an authority file and connects it to the resulting identifier, without replacing the local IRI.
- OpenRefine's built-in reconciliation client can query many different reconciliation services, not only Wikidata.
- Reconciled identifiers are added to the RDF mapping using ordinary vocabulary terms such as `schema:sameAs`, reused from the vocabularies already applied in the model and creation chapters.
- Reconciliation is rarely complete or fully automatic; reviewing candidate matches carefully remains the responsibility of the data creator.

::::::::::::::::::::::::::::::::::::::::::::::::::
