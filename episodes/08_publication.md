---
title: "Publish your Linked Data"
teaching: 15
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- Why does Linked Open Data only reach its full value once it is published?
- What is a simple way to publish RDF data online?
- What should we keep in mind when publishing data on GitHub?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain why publishing is a core part of Linked Open Data, not an optional extra step
- Describe how to publish an RDF file so that it has a stable, resolvable URL
- Name basic good practices for publishing data on GitHub

::::::::::::::::::::::::::::::::::::::::::::::::


## From a private model to Linked *Open* Data

So far, everything we built, from our first mind map to the Turtle and JSON-LD files we exported from OpenRefine and enriched through reconciliation, has stayed on our own computer. That is completely fine for learning and practicing, but it means our data is not yet **Linked Open Data** in any meaningful sense.

- **Open** means that our data is actually accessible to others. Anyone should be able to find it, fetch it, and (legally) reuse it.
- **Linked** means that our IRIs actually connect to something. Other datasets can point to our resources, and our resources can point to theirs.

Neither of these is possible as long as our data only exists on our own laptop. An IRI like `ex:SurugueLouis` is not truly linked to anything if nobody else can ever look it up. Publishing is what turns a private model into part of the wider Web of Data.

::::::::::::::::::::::::::::::::::::::: callout

### 5-star Open Data

A well-known way to visualise the concept of LOD is the **5-star Open Data scheme**, originally proposed by Tim Berners-Lee:

- ★ data is available on the web, in any format, under an open license
- ★★ it is available as structured data (e.g. a table, not a scanned image)
- ★★★ it uses a non-proprietary format (e.g. CSV instead of Excel)
- ★★★★ it uses IRIs, so that people can point at your individual data
- ★★★★★ it is linked to other people's data, to provide context

:::::::::::::::::::::::::::::::::::::::::::::::::::::

By the time we reach this episode, our RDF model already fulfils several of these stars. It uses IRIs, and, once we reuse vocabularies, it links to other data. But without the first star, actually publishing it openly on the web, none of that matters yet.


## Publishing with GitHub

There are many ways to publish Linked Open Data (dedicated triple stores, SPARQL endpoints, data portals). For getting started, we do not need any of that. A free GitHub account and repository is enough to give our data a real, stable, and citable place on the web.

::::::::::::::::::::::::::::::::::::::: callout

### What is GitHub?

[GitHub](https://github.com) is a web platform for hosting and sharing files under version control, most commonly used for software code, but just as suitable for datasets. A **repository** ("repo") is simply a folder of files with a history of changes. A repository can be **public** (visible and downloadable by anyone) or **private** (visible only to people you invite). For our purposes, a public repository is what turns a file on our computer into something the whole web can reach.

:::::::::::::::::::::::::::::::::::::::::::::::::::::

Let's do this with the file we actually produced. We already exported our OpenRefine mapping as Turtle, and after reconciliation, that export also carries `schema:sameAs` links to Wikidata. A block of it, for a single artist, looks like this:

```turtle
@prefix rdf: <http://www.w3.org/1999/02/22-rdf-syntax-ns#> .
@prefix rdfs: <http://www.w3.org/2000/01/rdf-schema#> .
@prefix schema: <https://schema.org/> .

<http://example.org/person/Surugue%2C+Louis>
    a schema:Person ;
    rdfs:label "Surugue, Louis"@en ;
    schema:description "French, Paris ca. 1686–1762 Grand Vaux" ;
    schema:sameAs <https://www.wikidata.org/wiki/Q5981497> .
```

This one exported file, let's call it `met-dataset.ttl`, already carries the result of everything we did in the previous chapters: the entities and relationships we modelled, the vocabularies we reused, and the authority links we added through reconciliation. Publishing it is the last step that turns it into genuine Linked *Open* Data.

**1. Create a GitHub account, if you do not already have one**

Go to [github.com/join](https://github.com/join), choose a username, and sign up with an email address. A free account is enough for everything we do in this lesson.

**2. Create a new public repository**

1. Once logged in, click the **+** icon in the top right corner of any GitHub page and select **New repository** (or go directly to [github.com/new](https://github.com/new)).
2. Give it a name, for example `met-collection-lod`.
3. Under *Visibility*, make sure **Public** is selected. A private repository is not open data, no matter how well-modelled it is.
4. Click **Create repository**.

**3. Add `met-dataset.ttl` to the repository**

1. On the new repository's page, click **Add file** → **Upload files**.
2. Drag `met-dataset.ttl` into the browser window, or click *choose your files* to select it from your computer. You can add the JSON-LD export alongside it, as an alternative serialization of the same graph.
3. Scroll down and click **Commit changes**.

**4. Add a license file**

1. On the repository's main page, click **Add file** → **Create new file**.
2. Name the file `LICENSE`. GitHub recognises this filename and shows a **Choose a license template** link, click it.
3. Pick a license, for example [CC0 1.0](https://creativecommons.org/publicdomain/zero/1.0/) to place the data fully in the public domain, or [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/) to require attribution. If you are unsure which one fits, [choosealicense.com](https://choosealicense.com/) is a good reference.
4. Commit the new file.

Without a license, nobody can be legally sure they are allowed to reuse the data, even once they can technically access it.

**5. Add a short README**

1. Click **Add file** → **Create new file** again and name it `README.md`.
2. Describe what the dataset contains, which vocabularies it uses (schema.org), and how it was produced (OpenRefine and RDF-Transform, reconciled against Wikidata). A few sentences are enough.
3. Commit the new file.

**6. Get the file's stable URL**

1. Click on `met-dataset.ttl` in the repository's file list to open it.
2. Click the **Raw** button above the file content.
3. The address now shown in your browser is the file's permanent, fetchable URL, for our example something like:

```text
https://raw.githubusercontent.com/your-username/met-collection-lod/main/met-dataset.ttl
```

Anyone, a person in a browser, or an RDF tool, can now fetch this exact URL and get our data back. Opening it shows the plain content of the Turtle file, exactly what an RDF tool would retrieve as well. This is what makes the data "open" in the first-star sense above: it is genuinely available on the web, to anyone, without asking us for a copy.




:::::: keypoints
- Linked Open Data only reaches its full value once it is actually published and can be accessed by others.
- The 5-star Open Data scheme shows that being "open" (available, licensed) is the foundation everything else builds on.
- A public GitHub repository is a simple way to give an RDF file a stable, fetchable URL.
- An open license and a short README turn a published file into data that others can confidently find and reuse.
::::::