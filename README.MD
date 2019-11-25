# DFKI Product Corpus

This repository contains the DFKI Product Corpus, a dataset of 174 English web pages and social media posts annotated for _product_ and _company_ named entities, and the relation _CompanyProvidesProduct_. The goal is to make extraction of non-standard, B2B products and relations from unstructured text easier and more reliable. The corpus is also annotated for coreference chains of companies and products.

You can find the full description of the corpus here: [https://www.dfki.de/web/forschung/projekte-publikationen/publikationen/publikation/9428/](https://www.dfki.de/web/forschung/projekte-publikationen/publikationen/publikation/9428/)

The corpus is provided in two formats - AVRO and JSON, using the train/test split described in the paper. For details on the schema used for storing annotations, see below.

 * [Product Corpus Version 1](v1_20180509)
 * [Product Corpus Version 2](v2_20190618)

Changes for Version 2:
 * Annotated 21 more documents, for a total of 174.
 * Created a train/dev/test split
 * Annotation change: phrases that are used like proper name products in certain contexts or enumerations even without being explicitly used in a CompanyProvidesProduct relation mention, e.g. "[drip chamber] segment", are now marked as products.
 * Annotation change: phrases clearly recognizable as a physical product, esp. in market descriptions where specific products are mentioned, e.g. "[fusion pumps]" in the "[IV equipment] market", are now marked as products.

## Use
The DFKI Product Corpus is released as [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/). If you use this data, you should cite the accompanying paper:

_A Corpus Study and Annotation Schema for Named Entity Recognition and Relation Extraction of Business Products. Saskia Schön, Veselina Mironova, Aleksandra Gabryszak and Leonhard Hennig. Proceedings of LREC, 2018._ [(bib)](paper.bib) [(pdf)](https://www.dfki.de/fileadmin/user_upload/import/9428_lrec_product_corpus.pdf)


## Format

The corpus consists of Documents which store the original text and all annotations, according to the following AVRO schema:

 * [document.avsc](document.avsc)

You can use the following JAVA tools to read the AVRO version of the corpus:

 * [Corpus Reader Tools](sdw-tools-1.0-SNAPSHOT.jar)

To read the corpus, use the following code snippet:

   ```java
   File inputFile = new File("train.avro");
   DataFileReader<Document> reader = AvroUtils.createReader(inputFile);
   while (reader.hasNext()) {
      Document doc = reader.next();
      // do something
   }

   ```

Each document contains a list of ConceptMentions, which correspond to Named Entities and other typed concepts (e.g. trigger phrases):

   ```java
   for (ConceptMention c : doc.getConceptMentions()) {
       String nerTag = c.getType();
       String value = c.getNormalizedValue();
       int start = c.getSpan().getStart();
       int end = c.getSpan().getEnd();
       String originalText = doc.getText().substring(start, end);
       // etc ...
   }
   ```

Similarly, you can retrieve RelationMentions:

   ```java
   for (RelationMention r : doc.getRelationMentions()) {
       String relationType = c.getName();
       int start = c.getSpan().getStart();
       int end = c.getSpan().getEnd();
       String originalText = doc.getText().substring(start, end);
       for (RelationArgument arg : r.getRelationArguments()) {
           String role = arg.getRole();
           ConceptMention c = arg.getConceptMention();
           // ...
       }
       // ...
   }
   ```

ConceptMentions and RelationMentions are stored at the document level, and for each sentence as well. You can access a sentence's list of RelationMentions using:

   ```java
   for (Sentence s : doc.getSentences()) {
       List<RelationMention> relationMentions = s.getRelationMentions();
       // ...
   }
   ```



## Annotation Guidelines

[Product Corpus Annotation Guidelines v1.0 (Feb 2018)](Product_Corpus_Annotation_Guidelines_Feb_2018_v1.0.pdf)

[Coreference Annotation Guidelines_v1.0 (Feb 2018)](Coreference_Guidelines.pdf)
