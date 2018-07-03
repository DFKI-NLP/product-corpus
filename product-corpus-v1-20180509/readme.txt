Convert to AVRO for dfki-lt-re-group.bitbucket.io:

Checkout product-corpus Stand 2018-05-09

de.dfki.lt.spree.util.Recon2Document mit spree/tap/tap-experiments/src/main/resources/smartdata/recon2document-productcorpus.properties (20180507), auch hier im Ordner als 20180509 getagged

Create Train/Test split:
de.dfki.lt.spree.flink.batch.DocumentTrainDevTestSplitJob  mit spree/tap/tap-experiments/src/main/resources/smartdata/trainTestSplit-productcorpus.properties (20180507), auch hier im Ordner als 20180509 getagged

Convert to JSON:
java -jar /home/leonhard/Dokumente/forschung/code/avro-tools-1.7.7.jar tojson --pretty train.avro > train.json
java -jar /home/leonhard/Dokumente/forschung/code/avro-tools-1.7.7.jar tojson --pretty test.avro > test.json



Not included in merged files:
8b9dff1e86912b03.xml -> duplicate of 6f94e28182b68986.xml
3fa1fd3ebe856424.xml -> too noisy html2text
1ce22cbc82bace92.xml -> sports news
68a09ac41ca6bad9.xml -> sports news
5ea730ca85d3404a.xml -> duplicate of 5d8c516807feddff.xml
ca11df67b58d9c10.xml -> no content
bfa2e4b7008ff132.xml -> no content
fc77b9463ae3655c.xml -> no content
efa6c37ccffabd30.xml -> no content
eaee7d30459f2b0b.xml -> car ad
e8a8e5713b037837.xml -> sports news
dffc28f00d18152f.xml -> sports news
d44382d8d5fae89d.xml -> irrelevant content
d4fd1b64421870b2.xml -> duplicate of 5d64dbade1a460ff.xml
c469a1e109e3fc2c.xml -> irrelevant content
ac8c61bcd860fde7.xml -> no content
29668950e41b60c7.xml -> no content
2576094dc4eb30f7.xml -> duplicate of d4883380c560ad71.xml
6981b042b1e499d0.xml -> no content
03861c8fdcdce75f.xml -> no content
792ebdd149825f58.xml -> no content
574bf043dacd9267.xml -> duplicate of 518937e339271e6d.xml
564b993234b907a8.xml -> sports news
521c88b496b3af86.xml -> no content
508fea126b59d587.xml -> no content
91b4edcacecae9b9.xml -> no content
8c9a268596fb077d.xml -> deutsch
sensor-doc-vico-bcec3a88-35b3-305a-a04c-6f0ff7d9dc7b.xml -> Reason: car sale ad
sensor-doc-vico-be6cc198-be4c-3205-8b99-56fb26ee6d15.xml -> Reason: car sale ad
sensor-doc-vico-cebf08d8-c867-3c87-a01a-be61a743055e.xml -> Reason: car sale ad
sensor-doc-vico-d047af1c-1a8b-3288-b685-378d149b3262.xml -> Reason: car sale ad
sensor-doc-vico-d63ba0e8-9e9f-3916-8445-56ff66d5e962.xml -> Reason: car sale ad
sensor-doc-vico-d7979b16-4e9a-30c7-ab01-5ab3dca4fb5c.xml -> Reason: car sale ad
sensor-doc-vico-dd7e66ae-deaa-3330-b9c2-e757c63917a9.xml -> Reason: car sale ad
sensor-doc-vico-e06564e9-4632-3861-aed5-04330b235632.xml -> Reason: car sale ad
sensor-doc-vico-ec965016-5ca4-3f9a-844c-596a7ac33d81.xml -> Reason: car sale ad
sensor-doc-vico-f3b965a9-be7e-3e22-a6a8-4b79f3fc65ce.xml -> Reason: car sale ad


