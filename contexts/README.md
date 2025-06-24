# Contexts

This directory contains context files to be used as @contexts in JSON-LD documents.

The idea behing introducting JSON-LD context definitions is to represent the above information in a natural way, preferably as close as possible 
to one's natural native language. On the other hand, the information arranged in records should be precise enough to be processed and correctly 
'understood' by software tools. This is why I tend to refer the elements of information to ontological terms (and, for instance, to add sense to 
attributes and their values).

Currently, contexts are used to provide mapping between fields in JSON document and relationships or concepts 
specified, defined or just introducted in ontologies or other systematic collections of terms for classification.

Currently the following context domains are available:

## Personal reading log

- **Objective**: the objective of this context is to describe the fields of the 'personal log' about books (such as novels) or other kinds of publications (such as short stories)
  that have been read by me (or potentially - by anyone).
- **Format**: The original format is YAML (and 1-to-1 JSON representation is available)
- **Fields**: The following information elements are defined for each record:

   1. author: the author of the work
   2. title: the title of the work
   3. type: the type/form of the work (it can be a book with a novel inside, but also can be a collection of items such as collection of poems, a single short story published in a journal, etc..)
   4. format: the form/medium of the book (either 'text' or 'audiobook')
   5. language: the language in which the book was read
   6. date: the date when the book was read (=the reading was finished)
   7. comment: a short note about the book, one or two sentences usually covering the first impressions after the book have been read.
   8. review: a more systematic, longer description of the book usually taking the form of a review with personal remarks. 
   9. keywords: keywords (optional) to be used if a position has some specific feature (e.g. is a mandatory reading or has won a prize)

- **Example**: The example record (English variant, YAML) is as follows:

```yaml
id: '#120'
author: Tony Judt
title: 'Postwar: A history of Europe since 1945'
type:
- PopularScienceWork
- Audiobook
inLanguage: en
dateRead: '2014-10-10'
comment: Magnificent work. Now I know a lot more about the world. And about Europe. And about Poland.
review: "Well, until having listened to this book I thought I know a lot about the recent history of Europe (after the war). What I knew 
         was a very limiting Polish perspective with some elements completely missing and explained from the Communists' Poland perspective.
         For example, I was aware of many 'reforms' which were introducted in Poland in late '40 and '50. What I didn't know was that most of them,
         if not all, we designed in Moscow in Soviet Union and were introduced similarily in all (or most) of Soviet block countries. 
         In this perspective I could understand better that Eastern block was not as independent as I might have thought and who was in charge."
```

- **Example**: The example record (Polish variant, YAML) is as follows:

```yaml
id: '#120'
autor: Tony Judt
tytuł: 'Postwar: A history of Europe since 1945'
typ:
- Tekst_popularnonaukowy
- Audiobook
język: en
data: '2014-10-10'
komentarz: Wspaniała. Wiem dużo więcej o świecie. O Europie. O Polsce.
recenzja: "Zanim przesłuchałem tę książkę myślałem, że wiem sporo o tym co się działo w powojennej Europie. A tu okazało się, że to co 
           wiedziałem to była ograniczona i ograniczająca perspektywa polska, jeszcze dodatkowo zniekształcona przez przemilczenia i przekłamania ery
           komunistycznej w Polsce. Przykładowo, pojąłem jak najróżniejsze 'reformy' wprowadzone we wczesnych latach, różne denominacje, walka z drobnym
           biznesem były zaprojektowane w Moskwie i systematycznie wprowadzane w innych krajach bloku komunistycznego (Bułgarii, na Węgrzech, w Czechosłowacji).
           A niepodległość była faktycznie tylko iluzoryczna (bez decyzyjności za to z flagą, hymnem i medalami na olimpiadzie 'dla Polski')."
```

### Application in a reading log

The ideas of a 'reading log' is a file which contains short notes about books that have been read.
A general structure of the YAML file of this kind is as follows:

```yaml
'@context': https://michalroj.github.io/ontologies/contexts/personal_reading_log_context_pl.jsonld
objects:
- RECORD 1
- RECORD 2
- RECORD 3
- etc.
```

Note that the IRI specified in the top line (as '@context') determined the variant of the vocabulary used in the RECORDs' descriptions.
The [above context](https://michalroj.github.io/ontologies/contexts/personal_reading_log_context_pl.jsonld) is a Polish variant of the context.
(In fact it is the same file as [the context file from this repository](personal_reading_log_context_pl.jsonld) but made available as a ready-to-be-used resource
from Github pages.)

Another variant of context would be [the English version of this context](personal_reading_log_context.jsonld). Then, the fields/attributes would be different.

In both cases, however, most of the attributes are mapped into the same ontology properties (schema.org in this case), such as 'schema:author', 'schema:name' or 'schema:inLanguage').

Example records for both variants are shown above (the Tony Judt's "Postwar" book).

An example with more records is shown [here in JSON-LD](../examples/read_books_zajdel_2024.jsonld) and [here in YAML-LD](../examples/read_books_zajdel_2024.yamld)
(this is the list of the [Zajdel award](https://en.wikipedia.org/wiki/Janusz_A._Zajdel_Award) nominees for 2024, the prize not yet won now).

What is important, in the records descriptions one can use the 'type' defined in the PublicationsFormsOntology (either [English version](../ontologies/PublicationsFormsOntology.ttl) 
or [Polish version](../ontologies/PublicationsFormsOntology_pl.ttl)), for instance, both 'PopularScienceWork' and 'Audiobook' classes come from this ontology (English variant).


## References to schema.org concepts

The proposed context files employ schema.org for most of the above fields:

- "http://schema.org/author": The author of this content or rating.
- "http://schema.org/name": The name given to the resource.
- "http://schema.org/inLanguage": The language of the content or performance or used in an action.
- "http://schema.org/dateRead": The date/time at which the message has been read by the recipient if a single recipient exists.
- "http://schema.org/comment": Comments, typically from users.
- "http://schema.org/review": A review of the item.
- "http://schema.org/keywords": Keywords or tags used to describe some item. Multiple textual entries in a keywords list are typically delimited by commas, or by repeating the property.

For 'type' and 'format' I employ a separate ontology (of my design) even if their meaning is close to:

- "http://schema.org/genre": Genre of the creative work, broadcast channel or group.
- "http://schema.org/bookFormat": The format of the book.

