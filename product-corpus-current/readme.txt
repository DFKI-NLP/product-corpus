Convert to AVRO for dfki-lt-re-group.bitbucket.io:

Checkout product-corpus Stand 2018-05-09

de.dfki.lt.spree.util.Recon2Document mit spree/tap/tap-experiments/src/main/resources/smartdata/recon2document-productcorpus.properties (20180507), auch hier im Ordner als 20180509 getagged

Create Train/Test split:
de.dfki.lt.spree.flink.batch.DocumentTrainDevTestSplitJob  mit spree/tap/tap-experiments/src/main/resources/smartdata/trainTestSplit-productcorpus.properties (20180507), auch hier im Ordner als 20180509 getagged

Convert to JSON:
java -jar /home/leonhard/Dokumente/forschung/code/avro-tools-1.7.7.jar tojson --pretty train.avro > train.json
java -jar /home/leonhard/Dokumente/forschung/code/avro-tools-1.7.7.jar tojson --pretty test.avro > test.json


Changes from Version 1 (20180509)
---------------------------------

Added annotations

 - phrases that are used like proper name products in certain contexts or enumerations even without being explicitly used in a CompanyProvidesProduct mention, e.g. "[drip chamber] segment"
 - phrases clearly recognizable as a physical product, esp. in market descriptions where specific products are mentioned, e.g. "[fusion pumps]" in the "[IV equipment] market".



