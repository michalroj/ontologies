# Contexts

This directory contains context files to be used as @contexts in JSON-LD documents.
Currently contexts are used to provide mapping between fields in JSON document and relationships or concepts 
specified, defined or just introducted in ontologies or other systematic collections of terms for classification.

Currently the following context documents are available:

## Personal reading log

**Objective**: the objective of this context is to describe the fields of the 'personal log' about books (such as novels or short stories) 
  that have been read by me (or potentially - by anyone).

  In my personal log I introduced the following fields:

  1. author: the author of the book
  2. title: the title of the book
  3. genre: the genre of the book
  4. inLanguage: the language in which the book was read
  5. bookFormat: the format of the book (printed or audiobook)
  6. dateRead: the date the book was read 
  7. comment: a short note about the book, one or two sentences usually covering the first impressions after the book have been read.
  8. review: a more systematic, longer description of the book usually taking the form of a review with personal remarks. 

 Context:
 In the file [personal_reading_log_context_lite.jsonld](personal_reading_log_context_lite.jsonld) there is the first version of the context specified using the concepts / relations
 taken from the schema.org and Dublin Core ontologies. In addition, there is also a Polish version of the context file 
 ([personal_reading_log_context_lite_pl.jsonld](personal_reading_log_context_lite_pl.jsonld)). The definitions of the fields are the same so
 their meaning can be interpreted properly in both cases.

 (This is a 'lite' version of the context which uses only well-known, well-established ontologies to describe fields' meaning. However, since those ontologies do not provide
  the ideal means for my to express full semantics and/or structure, more complex versions will be presented which would also offer more functionality). 

 The following schema.org/DC terms are used: 

 1. "http://schema.org/author": The author of this content or rating.
 2. "http://purl.org/dc/terms/title": The name given to the resource.
 3. "http://schema.org/genre": Genre of the creative work, broadcast channel or group.
 4. "http://schema.org/inLanguage": The language of the content or performance or used in an action.
 5. "http://schema.org/bookFormat": The format of the book.
 6. "http://schema.org/dateRead": The date/time at which the message has been read by the recipient if a single recipient exists.
 7. "http://schema.org/comment": Comments, typically from users.
 8. "http://schema.org/review": A review of the item.

 The meaning of the terms is close enough to the intention my fields (e.g. 'schema:author', 'schema:name' and 'schema:genre' are used in the https://schema.org/author example 
 in the very similar way). However, some comments below:
 
 Comments about the used items:

 1. "schema:author": this is good choice even if the proposed object (rangeIncludes) is 'Person'. I can use (for a while at least) the purely string-based author names.
                    maybe the string-based approach should be somehow expressed either in the 'context file' or in the data file (@id + @type)
 2. "dct:title": an alternative, used in the similar context would be "schema:name"
 3. "schema:genre": this seems ok however, "dcterms:type" and "dcat:theme" can be also used here
 4. "schema:inLanguage": this seems ok. The values should be rather 'en', 'pl' than full names. An alternative would be "dct:language"
 5. "schema:bookFormat": this seems ok, but the suggested values come from 'https://schema.org/BookFormatType'. I propose to use schema:AudiobookFormat and schema:Paperback,
                        even if the latter is used in the meaning of 'written form' as opposed to 'audio form' and can cover e-books as well.
 6. "schema:dateRead": this value has been designed for messages (SMS, instant messaging, etc.), however, finish of the book reading seems similar in meaning so this is used here.
 7. "schema:comment": this seem ok, even it not full previse regarding the content.
 8. "schema:review": Sometimes the content is less a review but a description, similar in meaning to "dct:description": description may include but is not limited to: 
                 an abstract, a table of contents, a graphical representation, or a free-text account of the resource.

Even if I tried to apply Dublin Core as much as I could, schema.org offered me more precise terms for this application. However, an alternative approach (and more complex) would be to
prepare custom ontologies with perfect semantics and labels in different languages (e.g. 'genres' or 'formats' might need update).

Good source for inspiration: https://www.w3.org/TR/vocab-dcat-2/ and https://www.w3.org/TR/vocab-dcat-3/

In addition, the @type might be used (e.g., as 'schema:Book') to define the type of the item in the database. In fact, sometimes it is not a book but a novella from a journal for instance
so I think more work is needed to think it out. Maybe we should not think about it as 'books' but as some more abstract resource,
perhaps http://purl.org/dc/terms/BibliographicResource or some element from https://www.w3.org/TR/vocab-dcat-2/ (or other ontology)
