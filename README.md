Jaccard Similarity Computation using Hadoop MapReduce

Overview

This project implements a Hadoop MapReduce program to compute the Jaccard Similarity between pairs of documents based on the words they contain. The Jaccard Similarity is calculated as:



where:

 and  are the sets of words in two different documents.

 represents the number of common words between the two documents.

 represents the total number of unique words across both documents.

Approach and Implementation

Mapper

The Mapper processes each line (representing a document), extracts the document ID and its words, and emits key-value pairs where the key is the document ID and the value is the set of words.

Reducer

The Reducer receives word sets for each document, computes Jaccard Similarity for each document pair, and outputs the similarity score.

Steps:

Tokenization: Split each document's text into words.

Pairwise Comparison: Compute similarity for all document pairs.

Aggregation: Calculate intersection and union sizes and compute similarity.

Final Output: Emit document pairs with their similarity scores.

Running the Project

Prerequisites

Java 8 or higher

Hadoop

Maven

Build the Project

mvn clean package

Upload Input Files to HDFS

hdfs dfs -mkdir -p /user/input
hdfs dfs -put input.txt /user/input

Run the MapReduce Job

hadoop jar target/jaccard-similarity.jar com.example.JaccardSimilarity /user/input /user/output

Retrieve the Output

hdfs dfs -cat /user/output/part-r-00000

Sample Input

doc1 hadoop is a distributed system
doc2 hadoop is used for big data processing
doc3 big data is important for analysis

Sample Output

Doc1, Doc2 Similarity: 0.44
Doc1, Doc3 Similarity: 0.10
Doc2, Doc3 Similarity: 0.20

Challenges and Solutions

Handling Large Datasets: Optimized by using efficient data structures for storing word sets.

Performance Bottlenecks: Used combiners to reduce shuffle overhead.

Debugging Hadoop Jobs: Used yarn logs to diagnose job failures.

Conclusion

This project demonstrates computing document similarity using Hadoop MapReduce, enabling scalable processing of large text datasets. The approach ensures efficient computation of pairwise document similarities with minimal memory overhead.

