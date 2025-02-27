## Prepare packages and dataset for pyspark

For simplicity export the location to these jars. All examples assume the packages and dataset will be placed in the `/opt/xgboost` directory:

### Download the jars

1. Download the XGBoost for Apache Spark jars
   * [XGBoost4j Package](https://repo1.maven.org/maven2/com/nvidia/xgboost4j_3.0/1.3.0-0.1.0/)
   * [XGBoost4j-Spark Package](https://repo1.maven.org/maven2/com/nvidia/xgboost4j-spark_3.0/1.3.0-0.1.0/)

2. Download the RAPIDS Accelerator for Apache Spark plugin jar
   * [RAPIDS Spark Package](https://repo1.maven.org/maven2/com/nvidia/rapids-4-spark_2.12/0.4.1/rapids-4-spark_2.12-0.4.1.jar)
  
   Then download the version of the cudf jar that your version of the accelerator depends on. Each cudf jar is for a specific version of CUDA and will not run on other versions.

     * [cuDF 11.0 Package](https://repo1.maven.org/maven2/ai/rapids/cudf/0.18.1/cudf-0.18.1-cuda11.jar)
     * [cuDF 10.2 Package](https://repo1.maven.org/maven2/ai/rapids/cudf/0.18.1/cudf-0.18.1-cuda10-2.jar)
     * [cuDF 10.1 Package](https://repo1.maven.org/maven2/ai/rapids/cudf/0.18.1/cudf-0.18.1-cuda10-1.jar)

### Build XGBoost Python Examples

Following this [guide](/getting-started-guides/building-sample-apps/python.md), you can get *samples.zip* and *main.py* and copy them to `/opt/xgboost`

### Download dataset

You need to download mortgage dataset to `/opt/xgboost` from this [site](https://rapidsai.github.io/demos/datasets/mortgage-data)

### Setup environments

``` bash
export SPARK_XGBOOST_DIR=/opt/xgboost
export CUDF_JAR=${SPARK_XGBOOST_DIR}/cudf-0.18.1-cuda10-1.jar
export RAPIDS_JAR=${SPARK_XGBOOST_DIR}/rapids-4-spark_2.12-0.4.1.jar
export XGBOOST4J_JAR=${SPARK_XGBOOST_DIR}/xgboost4j_3.0-1.3.0-0.1.0.jar
export XGBOOST4J_SPARK_JAR=${SPARK_XGBOOST_DIR}/xgboost4j-spark_3.0-1.3.0-0.1.0.jar
export SAMPLE_ZIP=${SPARK_XGBOOST_DIR}/samples.zip
export MAIN_PY=${SPARK_XGBOOST_DIR}/main.py
```
