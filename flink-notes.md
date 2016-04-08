# Notes and observations about flink. 


## Improving flinks k nearest neighbors algorithm 
* source: http://insightdataengineering.com/blog/flink-knn/ 
* kappa architecture - https://www.oreilly.com/ideas/questioning-the-lambda-architecture (interesting read). 
* Bounding box algorithm - recursively create bounding rectangles until each box contains atmost a threshold number of points. Find the neearest neighbours by recursively going down the tree and storing the nearest rectangles in heap. 

## references: 
* Summingbird - write your code using this higher level framework and then it “compiles down” to stream processing or MapReduce under the covers.
* reprocessing previously processed data -  http://samza.apache.org/learn/documentation/0.7.0/jobs/reprocessing.html
* Apache Samza - http://samza.apache.org/learn/documentation/0.7.0/introduction/background.html
