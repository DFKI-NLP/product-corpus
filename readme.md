# DFKI Product Corpus

This repository contains the DFKI Product Corpus, a dataset of English web pages and social media posts annotated for _product_ and _company_ named entities, and the relation _CompanyProvidesProduct_. The goal is to make extraction of non-standard, B2B products and relations from unstructured text easier and more reliable. The corpus is also annotated for coreference chains of companies and products.

You can find the full description of the corpus here: [http://www.dfki.de/lt/publication_show.php?id=9428](http://www.dfki.de/lt/publication_show.php?id=9428)

The corpus is provided in two formats - AVRO and JSON, using the train/test split described in the paper. For details on the schema used for storing annotations, see below.

 * [Product Corpus (AVRO)](downloads/product-corpus-avro.zip)
 * [Product Corpus (JSON)](downloads/product-corpus-json.zip)

## Use
The DFKI Product Corpus is released as [CC-BY 4.0](https://creativecommons.org/licenses/by/4.0/). If you use this data, you should cite the accompanying paper:

_A Corpus Study and Annotation Schema for Named Entity Recognition and Relation Extraction of Business Products. Saskia Schön, Veselina Mironova, Aleksandra Gabryszak and Leonhard Hennig. Proceedings of LREC, 2018._ [(bib)](downloads/paper.bib) [(pdf)](http://www.dfki.de/web/forschung/iwi/publikationen/renameFileForDownload?filename=lrec_product_corpus.pdf&file_id=uploads_3519)


## Format

The corpus consists of Documents which store the original text and all annotations, according to the following AVRO schema:

 * [document.avsc](downloads/document.avsc)

You can use the following JAVA tools to read the AVRO version of the corpus:

 * [Corpus Reader Tools](downloads/sdw-tools-1.0-SNAPSHOT.jar)

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

[Product Corpus Annotation Guidelines v1.0 (Feb 2018)](downloads/Product_Corpus_Annotation_Guidelines_Feb_2018_v1.0.pdf)

[Coreference Annotation Guidelines_v1.0 (Feb 2018)](downloads/Coreference_Guidelines.pdf)
