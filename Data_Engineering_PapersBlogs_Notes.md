### Medium:
	
# Data pipelines, Luigi, Airflow: everything you need to know*

Link : https://towardsdatascience.com/data-pipelines-luigi-airflow-everything-you-need-to-know-18dc741449b7
Description: Detailed comparision of two Workflow Management Systems (WMS) Apache Airflow and Luigi.
Technologies: Apache Airflow, Luigi. 
More: In Airflow, a workflow is defined as a collection of tasks with directional dependencies, basically a directed acyclic graph (DAG). Each node in the graph is a task, and edges define dependencies among the tasks. The main components of Airflow are: 1) Metadata Database (i.e Postgres), 2) Scheduler, 3) Executor. The metadata database stores the state of tasks and workflows. The scheduler uses the DAGs definitions, together with the state of tasks in the metadata database, and decides what needs to be executed. The executor is a message queuing process (usually Celery) which decides which worker will execute each task. No information is shared between tasks, the maximum possbile parallelisation. Tasks do not communicate; has its own scheduler; very nice UI.
Luigi is a python package to build complex pipelines and it was developed at Spotify and it consist of two main parts: Tasks and Targets. It’s generally based on pipelines, tasks input and output share information and is connected together and exploits Target-based approach. No user interaction with running processes; absent of triggering.


### Trivago:

# Accomodation Consilidation: How we created an ETL pipeline on cloud 
	
Link: https://tech.trivago.com/2020/03/26/accommodation-consolidation-how-we-created-an-etl-pipeline-on-cloud/	
Description: How to process millions of updates simulataneously. 
Technologies:  AWS Glue (ELT tool) and AWS Step Functions (orchestration service).
More: Initially, authors had two proposals for the technologies to be used. The AWS Glue because it can process a huge amount of data. AWS Glue is a fully managed ETL service provided by AWS that uses Apache Spark clusters underneath, which seemed perfect to process the large number of updates. Additionally AWS Step Functions was picked because it provides more flexibility in plugging new models. AWS Step Functions is a tool to orchestrate different AWS services, which is ideal to accomplish the flexibility we require. At the end of the prototyping phase, we realized that these two technologies have both benefits and drawbacks for our use-case, hence a hybrid solution using both AWS Glue and AWS Step Functions.
		
# Getting Ready For The Big Data Apocalypse 
	
Link: https://tech.trivago.com/2019/12/16/getting-ready-for-the-big-data-apocalypse/
Description: Exponential data growth and how to deal with it. 
Technologies: Apache Kudo (storage), Apache Impala (SQL engine), Kotlin, gRPC (microservices management).
More: Data storage - Apache Kudo (open source columnar storage system developed for the Apache Hadoop) that supports BI on Hadoop (but doesn’t provide an SQL engine). Therefore we decided to implement Impala as an SQL engine, which matches perfectly with Kudu and the whole Hadoop ecosystem. The project architecture is based on microservices architecture, which, put simply, splits the project into small independent pieces of code that share the same business logic.
		
# Teardown, Rebuild: Migrating from Hive to PySpark
	
Link: https://tech.trivago.com/2018/12/03/teardown-rebuild-migrating-from-hive-to-pyspark/
Description: Migration of bidding platform from Hive to Spark.
Technologies: Apache Hadoop, Apache Hive (HQL), Apache Spark (PySpark), Unit-tests
More: The first version of the value-per-click (VPC) algorithm consisted of a data-pipeline that crunched data to update our VPC probability distributions by reading/writing tabular data into the Hadoop Distributed File System (HDFS) with Apache Hive, an SQL dialect that translates SQL into efficient MapReduce jobs. This worked well as long as we stuck to a simple Bayesian model to calculate the VPC and simple heuristics in the bidding layer. However, Hive was not a stable option to develop the bidding system we dreamed of during our sprint plannings, because of the lack of expressiveness of Hive’s SQL dialect, Unit-Tests etc. We tried different ways to write unit tests for Hive code with little success: Unit-tests on most existing frameworks must be written in Java (was not an option). The solution is - Spark with it amount of high-functional APIs to Scala, Python, R, and Java. Eventually the combination of Python+Spark was chosen.



		