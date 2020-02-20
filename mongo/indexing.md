# Using Indexes

## Features

* Indexes can be used to speed up sorting. Using sorted without indexing will just take the whole collection in memory and sort, which will increase your memory usage

* For compound indexes, sorting can use that index from left to right. For example if a compound index is `age_1_gender`, sorting by age will use that index, but if you sort with gender only it will go through all the docs as it's not indexed
* `_id` is indexed by default

* Partial Indexing
    * Use partial indexing to index just a subset of the collection; ie: age > 60 only. that will decrease your index size which will speed up your queries.
    * typically are used with hot subsets

## Caveats

* Indexes should be easy to sort (integer, short text), cause sorting and searching becomes harder and takes longer. So longer the index, the slower our reading and writing.

* If we have an index over a value, and a query to that value but it almost return the majority of the documents in the collection. In that case, the index just slow things down because it ran over the majority of the index collection then over the whole actual documents.

* A complex search should reduce the selection candidates as much as possible with the first item in the list of indexes. ‘Cardinality’ is the term used for this sort of selectivity. A field with low cardinality, such as gender is far less selective than surname. In our example, the surname is selective enough to be the obvious choice for the first field that is listed in an index, but not many queries are that obvious. Hence, Order of fields in the compound index, is very important. 

* Mongo treats null values as a value, meaning unique indexes can't have two null values
    * To Fix this we use unique index in conjunction with partial index. `db.users.createIndex({email: 1}, {unique: 1, paritalExpression: {email: {$exists: true}}})` to apply the unique index if only email field exists

* TTL index 
    * only works on date fields, and a single field. no compund indexes supported
    * adding the index will re-evaluate already inserted docs
    * `db.sessions.createIndex({createdAt: 1}, {expireAfterSeconds: 10})

