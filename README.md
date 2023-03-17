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

