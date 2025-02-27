Get Started with XGBoost4J-Spark with Apache Toree Jupyter Notebook
===================================================================

This is a getting started guide to XGBoost4J-Spark using an [Apache Toree](https://toree.apache.org/) Jupyter notebook. At the end of this guide, the reader will be able to run a sample notebook that runs on NVIDIA GPUs.

Before you begin, please ensure that you have setup a [Spark Standalone Cluster](/getting-started-guides/on-prem-cluster/standalone-scala.md).

It is assumed that the `SPARK_MASTER` and `SPARK_HOME` environment variables are defined and point to the master spark URL (e.g. `spark://localhost:7077`), and the home directory for Apache Spark respectively.

1. Make sure you have jupyter notebook installed first.
2. Build the 'toree' locally to support scala 2.12, and install it.

    ``` bash
    # Clone the source code
    git clone --recursive git@github.com:firestarman/incubator-toree.git -b for-scala-2.12

    # Build the Toree pip package. You can change "BASE_VERSION" to any version since it is used locally only.
    cd incubator-toree
    env BASE_VERSION=0.5.0 make pip-release

    # Install Toree
    pip install dist/toree-pip/toree-0.5.0.tar.gz
    ```

3. Prepare packages and dataset.

    Make sure you have prepared the necessary packages and dataset by following this [guide](/getting-started-guides/prepare-package-data/preparation-scala.md)

4. Install a new kernel with gpu enabled and lunch

    ``` bash
    jupyter toree install                                \
    --spark_home=${SPARK_HOME}                             \
    --user                                          \
    --toree_opts='--nosparkcontext'                         \
    --kernel_name="XGBoost4j-Spark"                         \
    --spark_opts='--master ${SPARK_MASTER} \
      --jars ${CUDF_JAR},${RAPIDS_JAR},${SAMPLE_JAR}       \
      --conf spark.plugins=com.nvidia.spark.SQLPlugin  \
      --conf spark.executor.extraClassPath=${CUDF_JAR}:${RAPIDS_JAR} \
      --conf spark.rapids.memory.gpu.pooling.enabled=false \
      --conf spark.executor.resource.gpu.amount=1 \
      --conf spark.task.resource.gpu.amount=1 \
      --conf spark.executor.resource.gpu.discoveryScript=./getGpusResources.sh \
      --files $SPARK_HOME/examples/src/main/scripts/getGpusResources.sh'
    ```

    Launch the notebook:

    ``` bash
    jupyter notebook
    ```

    Then you start your notebook and open [`mortgage-gpu.ipynb`](/examples/notebooks/scala/mortgage-gpu.ipynb) to explore.
