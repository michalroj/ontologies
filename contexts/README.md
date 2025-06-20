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
  9. keywords: keywords (optional) to be used if a position has some specific feature (e.g. is a mandatory reading or has won a prize)

### The 'light' version approach

 Context:
 In the file [personal_reading_log_context_lite.jsonld](personal_reading_log_context_lite.jsonld) there is the first version of the context specified using the concepts / relations
 taken from the schema.org ontology. In addition, there is also a Polish version of the context file 
 ([personal_reading_log_context_lite_pl.jsonld](personal_reading_log_context_lite_pl.jsonld)). The definitions of the fields are the same so their meaning can be interpreted properly in both cases.

 This is a 'lite' version of the context which uses only well-known, well-established ontologies to describe fields' meaning. However, since these ontologies do not provide
 the ideal means for my to express full semantics and/or structure, more complex versions are need to offer more functionality (ref. sections below). 

 The following schema.org terms are used in the above context: 

 1. "http://schema.org/author": The author of this content or rating.
 2. "http://schema.org/name": The name given to the resource.
 3. "http://schema.org/genre": Genre of the creative work, broadcast channel or group.
 4. "http://schema.org/inLanguage": The language of the content or performance or used in an action.
 5. "http://schema.org/bookFormat": The format of the book.
 6. "http://schema.org/dateRead": The date/time at which the message has been read by the recipient if a single recipient exists.
 7. "http://schema.org/comment": Comments, typically from users.
 8. "http://schema.org/review": A review of the item.
 9. "http://schema.org/keywords": Keywords or tags used to describe some item. Multiple textual entries in a keywords list are typically delimited by commas, or by repeating the property.

 The meaning of the terms is close enough to the intention my fields (e.g. 'schema:author', 'schema:name' and 'schema:genre' are used in the https://schema.org/author example 
 in the very similar way). In addition, almost all above attributes (except 'schema:dateRead') are actually part of the 'schema:Book' objects.

 Anyway, some comments below:
 
 1. "schema:author": this is good choice even if the proposed object (rangeIncludes) is 'schema:Person'. I can use (for a while at least) the purely string-based author names.
                    maybe the string-based approach should be somehow expressed either in the 'context file' or in the data file (@id + @type)
 2. "schema:name": an alternative, used in the similar context would be "dct:title" (title sounds better, but 'schema:name' is used exactly in this context)
 3. "schema:genre": this seems ok however, "dcterms:type" and "dcat:theme" can be also used here
 4. "schema:inLanguage": this seems ok. The values should be rather 'en', 'pl' than full names. An alternative would be "dct:language"
 5. "schema:bookFormat": this seems ok, but the suggested values come from 'https://schema.org/BookFormatType'. I propose to use schema:AudiobookFormat and schema:Paperback,
                        even if the latter is used in the meaning of 'written form' as opposed to 'audio form' and can cover e-books as well.
 6. "schema:dateRead": this value has been designed for messages (SMS, instant messaging, etc.), however, finishing of the book reading seems similar in meaning so this is used here.
                       an alternative attribute which is in the 'schema:Book' class would be 'schema:contentReferenceTime', 'schema:sdDatePublished', with the earlier having closer semantics
 7. "schema:comment": this seems ok, even if not fully expressing the 'short note' in our meaning.
 8. "schema:review": Sometimes the content is less a review but a description, similar in meaning to "dct:description"
 9. "schema:keywords": this seems ok. Has to be tested more.

Even if I tried to apply Dublin Core as much as I could, schema.org offered me more precise terms for this application. However, an alternative approach (and more complex) would be to
prepare custom ontologies with perfect semantics and labels in different languages (e.g. 'genres' or 'formats' might need update).

Good source for inspiration: https://www.w3.org/TR/vocab-dcat-2/ and https://www.w3.org/TR/vocab-dcat-3/

In addition, the @type might be used (e.g., as 'schema:Book') to define the type of the item in the database. In fact, sometimes it is not a book but a novella from a journal for instance
so I think more work is needed to think it out. Maybe we should not think about it as 'books' but as some more abstract resource,
perhaps http://purl.org/dc/terms/BibliographicResource or some element from https://www.w3.org/TR/vocab-dcat-2/ (or other ontology)

**Examples of the JSON-LD data files**

#### English version

```
{
      "@id": "#11",
      "@type": "schema:Book",
      "author": "Michael Chabon",
      "title": "Cudowni chłopcy",
      "genre": "powieść",
      "inLanguage": "Polski",
      "bookFormat": "schema:Paperback",
      "dateRead": "2009-09-05",
      "comment": "Bardzo dobra",
      "review": ""
}
```

#### Polish version

```
{
      "@id": "#11",
      "@type": "schema:Book",
      "autor": "Michael Chabon",
      "tytuł": "Cudowni chłopcy",
      "typ": "powieść",
      "język": "Polski",
      "medium": "schema:Paperback",
      "data": "2009-09-05",
      "komentarz": "Bardzo dobra",
      "recenzja": ""
}
```

### The 'full' version approach


In this version of the context we still have nine fields with the meaning presented above, however for some fields we provide vocabulary which can be easily used by in the final documents.
In addition to more precise vocabulary we introduce means for simplification of the JSON-LD file to make it look more like an ordinary JSON file. 
Finally, we introduce the means to use the keywords (or, in fact, ontology terms) without prefixes in national languages so the final document might be get a pleasant national language form.

The context file (for Polish) is here: [personal_reading_log_context_pl.jsonld](personal_reading_log_context_pl.jsonld).

Example entry for Polish:

```
    {
      "ID": "#11",
      "typ": "Powieść",
      "autor": "Michael Chabon",
      "tytuł": "Cudowni chłopcy",
      "język": "Polski",
      "data": "2009-09-05",
      "komentarz": "Bardzo dobra",
      "recenzja": ""
    }
```

The values of 'typ' (such as "Powieść") are now the vocabulary from the ontology 
[https://michalroj.github.io/ontologies/ontologies/PublicationFormsOntology_pl.owl](https://michalroj.github.io/ontologies/ontologies/PublicationFormsOntology_pl.owl) 
so they can be processed using semantic tools thus gaining more value comparing to a the 'lite' approach.

In addition, there is an 'Audiobook' class defined in the ontology so is someone needs to express that the read book variant was in audio form, he can express it as follows:

```
    {
      "ID": "#11",
      "typ": [ "Powieść", "Audiobook" ]
      "autor": "Michael Chabon",
      "tytuł": "Cudowni chłopcy",
      "język": "Polski",
      "data": "2009-09-05",
      "komentarz": "Bardzo dobra",
      "recenzja": ""
    }
```

#### For reference, the version 1 context (will be removed)

The context file (for Polish) is here: [personal_reading_log_context_v1_pl.jsonld](personal_reading_log_context_v1_pl.jsonld).

Example entry for Polish:

```
    {
      "ID": "#11",
      "szablon": "Książka",
      "autor": "Michael Chabon",
      "tytuł": "Cudowni chłopcy",
      "typ": "Powieść",
      "język": "Polski",
      "medium": "Tekst",
      "data": "2009-09-05",
      "komentarz": "Bardzo dobra",
      "recenzja": ""
    }
```

The values of 'typ' (such as "Powieść") and values of 'medium' (such as "Tekst") and also from 'szablon' (such as "Książka") are now the vocabulary
from the ontology https://michalroj.github.io/ontologies/ontologies/BooksTypesGenresAndStylesOntology_pl.owl so they can be processed using semantic tools thus
gaining more value from the reading record base.
