# send-graphite-protocol-telemetry
Mechanisms to send graphite protocol based telemetry data to various sinks

**Literature**

Sending telemetry can happen via **Push** or **Pull** based mechanism and sometimes it is a combination of both, it highly depends on these factors:
1. Latency constraints.
2. Complexity of monitoring setup.
3. Nature of resource i.e. ephemeral or not.
4. Scalability.
5. Error handling and Reliability.
6. Freshness of data/Real time data.
7. Existing Infrastructure setup.
8. Expertise within team.
9. Network constraints.


### Push Based Mechanisms

* [Using vmagent send spark jobs telemetry](https://github.com/pree-dew/send-graphite-based-telemetry/blob/main/push-mechanisms/spark-application-via-vmagent/Readme.md)

   
  

   
