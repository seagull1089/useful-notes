# python pandas tips and notes. 
* pandas summary : ```pip install  pandas-summary``` can give some really nice statistics about the data in the dataframe. refer to  https://github.com/mouradmourafiq/pandas-summary
* spark pandas scalar iterator UDF: 
```python 
from typing import Iterator, Tuple

@pandas_udf("double")
def predict(iterator: Iterator[pd.DataFrame]) -> Iterator[pd.Series]:
  model_path = f"runs:/{run.info.run_id}/random-forest-model" 
  model = mlflow.sklearn.load_model(model_path) # Load model
  for features in iterator:
    pdf = pd.concat(features, axis=1)
    yield pd.Series(model.predict(pdf))

prediction_df = sparkDF.withColumn("prediction", predict(*sparkDF.columns))
display(prediction_df)
```
* spark pandas function API: 
```python
def predict(iterator: Iterator[pd.DataFrame]) -> Iterator[pd.DataFrame]:
  model_path = f"runs:/{run.info.run_id}/random-forest-model" 
  model = mlflow.sklearn.load_model(model_path) # Load model
  for features in iterator:
    yield pd.concat([features, pd.Series(model.predict(features), name="prediction")], axis=1)
    
display(sparkDF.mapInPandas(predict, """`host_total_listings_count` DOUBLE,`neighbourhood_cleansed` BIGINT,`latitude` DOUBLE,`longitude` DOUBLE,`property_type` BIGINT,`room_type` BIGINT,`accommodates` DOUBLE,`bathrooms` DOUBLE,`bedrooms` DOUBLE,`beds` DOUBLE,`bed_type` BIGINT,`minimum_nights` DOUBLE,`number_of_reviews` DOUBLE,`review_scores_rating` DOUBLE,`review_scores_accuracy` DOUBLE,`review_scores_cleanliness` DOUBLE,`review_scores_checkin` DOUBLE,`review_scores_communication` DOUBLE,`review_scores_location` DOUBLE,`review_scores_value` DOUBLE, `prediction` DOUBLE""")) 
``` 
or 
```python
from pyspark.sql.functions import lit
from pyspark.sql.types import DoubleType

schema = sparkDF.withColumn("prediction", lit(None).cast(DoubleType())).schema
display(sparkDF.mapInPandas(predict, schema)) 
```
