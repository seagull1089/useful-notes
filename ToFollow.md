## Delite DSL http://stanford-ppl.github.io/Delite/
* Provides DSL for various domains. 
* OptiML for machine learning tasks. 
* DSL built on top of scala. Note: cannot intermix scala with the the optiML code. 
```
untilConverged(kMeans, tol){ kMeans => 

 val clusters = samples.groupBy { sample => 
  kMeans.mapRows(mean => dist(sample, mean)).minIndex
 }
 val newKMeans = clusters.map( c= > c.sum/ .. )
 newKMeans
} 

```
* Markov state models. 
* To follow up: What is the advantage of using this framework. 
 
