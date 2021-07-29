# python pandas tips and notes. 
* pandas summary : ```pip install  pandas-summary``` can give some really nice statistics about the data in the dataframe. refer to  https://github.com/mouradmourafiq/pandas-summary
* spark pandas scalar iterator UDF: ``` from typing import Iterator, Tuple

@pandas_udf("double")
def predict(iterator: Iterator[pd.DataFrame]) -> Iterator[pd.Series]:
  model_path = f"runs:/{run.info.run_id}/random-forest-model" 
  model = mlflow.sklearn.load_model(model_path) # Load model
  for features in iterator:
    pdf = pd.concat(features, axis=1)
    yield pd.Series(model.predict(pdf))

prediction_df = sparkDF.withColumn("prediction", predict(*sparkDF.columns))
display(prediction_df)```
