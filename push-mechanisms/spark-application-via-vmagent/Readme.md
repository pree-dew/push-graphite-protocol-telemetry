
### 1. Via vmagent

Taking an example set up for hadoop and spark where metrics generated via spark jobs needs to sent via **graphite** protocol.

**Set up - Push Based**


  <img width="809" alt="Screenshot 2024-07-17 at 4 45 42 PM" src="https://github.com/user-attachments/assets/2a9be30b-4a1b-4c26-b32c-780ff1475df0">

- Setup `hadoop` and `apache-spark` as per your machine OS.

- Setup `vmagent` and `victoriametrics`(prometheus compatible backend) by:
  

   `
   cd graphite-via-spark
   `
  
   `
   docker-compose up
   `
  
   **Note**:

  All commands are compatible as per the setup of `docker-compose` and other configuration given in this example,
  for your production setup it will be different
  

   **Highlight:**

   - Here vmagent is running with `graphite` mode and a relabel config is used to change `.` and `-` to `_`

   - If you want to `validate` that `vmagent` and `victoriametrics` setup is working find you can send use this
   command 

    ```
    echo "test_metric_name 60 $(date +%s)" | nc localhost 2003
    ```
  
    Move to [Victoriametrics UI](http://localhost:8439/vmui) and run query

    ```
    test_metric_name{}
    ```
  
- Configure spark to send metrics
    - Create a metrics.properties file in $SPARK_HOME/conf:
      
      ```
      *.sink.graphite.class=org.apache.spark.metrics.sink.GraphiteSink
      *.sink.graphite.host=localhost # in production it will be vmagent host 
      *.sink.graphite.port=2003  # in production it will be port of vmagent on which graphite protocol is enabled
      *.sink.graphite.prefix=spark # can be any prefix
      *.sink.graphite.period=5
      *.sink.graphite.unit=seconds
- Run a spark job, ex:

  `spark-submit --class org.apache.spark.examples.SparkPi --master yarn --deploy-mode client $SPARK_HOME/examples/jars/spark-examples_2.12-3.0.0.jar 10
  `

- Move to [Victoriametrics UI](http://localhost:8439/vmui) and run query starting with metric starting with `spark`, ex:

  **Note: application id in screenshot will vary as per your application id**
  
  
<img width="1344" alt="Screenshot 2024-07-17 at 5 34 06 PM" src="https://github.com/user-attachments/assets/4c15e9f8-7606-4322-b6a2-f2c1c580ceb7">



   
