# Contexts

This directory contains context file to be used as @contexts in JSON-LD documents.
Currently contexts are used to provide mapping between fields in JSON document and relationships or concepts 
specified, defined or just introducted in ontologies or other systematic collections of terms for classification.

Currently the following context documents are available:

# Personal reading log

Objective: the objective of this context is to describe the fields of the 'personal log' about books (such as novels or short stories) 
  that have been read by me (or potentially - by anyone).

  In my personal log I introduced the following fields:

  - author: the author of the book
  - title: the title of the book
  - genre: the genre of the book
  - inLanguage: the language in which the book was read
  - bookFormat: the format of the book (printed or audiobook)
  - dateRead: the date the book was read 
  - firstImpression: a short note about the book, one or two sentences usually covering the first impressions after the book have been read.
  - description: a description of the book usually taking the form of a review with personal remarks. 

 Context:
 In the following file 'personal_reading_log_context.jsonld' there is a first version of the context specified using the concepts / relations
 taken from the schema.org ontology.
 The following schema.org terms are used: 
 - "schema:author"
 - "schema:name"
 - "schema:genre"
 - "schema:inLanguage"
 - "schema:bookFormat"
 - "schema:dateRead"
 - "schema:description"
 - "schema:comment"

 Even if their meaning is close to the intention my fields (e.g. 'schema:author', 'schema:name' and 'schema:genre' are used in the https://schema.org/author example 
 in the very similar way) some fields will need refinement (perhaps the schema.org terms do not have appropriate terms for expressing the fields I need).
 

