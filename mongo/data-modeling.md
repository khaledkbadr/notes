# How to model your Data into MongoDB?

## Guidelines

For starters you have to perform the below steps before you start defining your schema, to have a clear idea about what you're building

* Define the data/fields you need; and how they relate with each other
* Define your collections and fields grouping
* Define how will you query your data
* Define whether you should optimize for read or write

## Defining Schema

Now we move to they types of relations between data and whether to use embedding or refernce for relations

* 1-1 relation
    * Embedding: we use embedding in one to one relations when you have a huge number of documents because querying on that number will take time.For example: a patient has only one disease summary, if refernce is used here, we will have make two queries to fetch the summary and having a huge number of summaries will only increase query latency

    * Reference: we use reference if we want to query or analyize the documents separately without using the relation. For example: for person who purchase car, we usually fetch cars and analyze them without using their relationship with the person who bought them

* 1-N Relation
    * Embedding: Same as 1-1 Relation
    * Reference: if the embedded docs is huge and can exceed the 16 MB restriction 


* M-N Relation
    * Embedded: if we don't need Consistency. For example a purchase of products shouldn't be affected by a change in the product itself.
    * Reference: If we will have a lot of duplications; and hence a lot of places to change if any change happened.


