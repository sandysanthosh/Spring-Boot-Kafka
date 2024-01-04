# Spring-Boot-Kafka

#### Spring Boot Kafka code:

```

<dependency>
  <groupId>org.springframework.kafka</groupId>
  <artifactId>spring-kafka</artifactId>
  <version>2.8.0</version>
</dependency>


```

2. Create a Kafka producer:

```

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.kafka.core.KafkaTemplate;
import org.springframework.stereotype.Component;

@Component
public class KafkaProducer {

    private static final String TOPIC = "my-topic";

    @Autowired
    private KafkaTemplate<String, String> kafkaTemplate;

    public void sendMessage(String message) {
        kafkaTemplate.send(TOPIC, message);
    }
}

```

3. Create a Kafka consumer:

```

import org.springframework.kafka.annotation.KafkaListener;
import org.springframework.stereotype.Component;

@Component
public class KafkaConsumer {

    private static final String TOPIC = "my-topic";

    @KafkaListener(topics = TOPIC, groupId = "group_id")
    public void consume(String message) {
        System.out.println("Consumed message: " + message);
    }
}

```

4. Configure Kafka in your application.yml file:

```

spring:
  kafka:
    bootstrap-servers: <your-kafka-bootstrap-server>
    
```

5. Use the Kafka producer to send a message:

```

@RestController
@RequestMapping("/kafka")
public class KafkaController {

    @Autowired
    private KafkaProducer producer;

    @PostMapping("/publish")
    public void sendMessage(@RequestBody String message) {
        producer.sendMessage(message);
    }
}

```

That's it! With these steps, you should be able to produce and consume Kafka messages in your Spring Boot application.

Note that you may need to modify some of the configurations to match your specific use case.



Sure, here's a quick overview of Apache Kafka:

### What is Kafka?

Apache Kafka is an open-source distributed event streaming platform used for building real-time data pipelines and streaming applications. It is designed to handle high-throughput, fault-tolerant, and scalable data streams.

### Core Concepts:

1. **Topics:** Data streams are organized into topics, which are the fundamental unit of data storage in Kafka. Producers publish messages to topics, and consumers subscribe to these topics to consume the messages.

2. **Partitions:** Each topic is divided into one or more partitions, which are individual ordered logs. Partitions allow data within a topic to be distributed across multiple servers, enabling parallel processing and scalability.

3. **Producers:** Producers are responsible for publishing messages to Kafka topics. They push messages to specific topics, which are then distributed across partitions by Kafka.

4. **Consumers:** Consumers subscribe to topics and pull messages from Kafka partitions. Multiple consumer groups can independently read from the same topic, allowing parallel processing of data.

5. **Brokers:** Kafka clusters consist of multiple servers called brokers. Brokers store and manage the partitions, handle message replication, and ensure fault tolerance.

6. **ZooKeeper:** ZooKeeper is used by Kafka for cluster coordination, metadata management, and leader election. However, recent Kafka versions have moved away from direct ZooKeeper dependency in favor of an internal metadata quorum.

### Key Features:

- **Scalability:** Kafka is horizontally scalable and can handle a high volume of messages by distributing data across multiple brokers.
  
- **Durability:** Messages in Kafka are persisted on disk and replicated across multiple brokers, ensuring fault tolerance and data durability.

- **Real-time Stream Processing:** It supports real-time data processing and integration with various streaming frameworks like Apache Flink, Spark Streaming, etc.

### Key Components:

- **Producer API:** Allows applications to publish messages to Kafka topics.
  
- **Consumer API:** Enables applications to subscribe to topics and consume messages.
  
- **Streams API:** Provides a high-level abstraction for building stream processing applications that can consume input streams, perform processing, and produce output streams.

### Typical Use Cases:

- **Log Aggregation:** Collecting and aggregating log data from various sources.
  
- **Real-time Analytics:** Processing and analyzing streaming data for immediate insights.
  
- **Messaging System:** Building high-throughput message queues and data pipelines.

Learning Kafka involves understanding these concepts and components, working with its APIs, setting up clusters, creating producers and consumers, and exploring the various configurations for optimization and reliability. There are official documentation, tutorials, and community resources available for a deeper dive into Apache Kafka.



