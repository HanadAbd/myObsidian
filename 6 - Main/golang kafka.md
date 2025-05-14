	2025-01-03 13:35

Status:

Tags: [[Go Golang Learning]]

---


Apache Kafka is a system used stream messages.

For golang, you can use "github.com/IBM/sarama"

Requirements for Kafka stream:
--
Broker - This is the server that Kafka messages are served/streamed from and Kafka messages are stored.
Topic  A stream of records on the broker that are partionied for scalability 
Producer -  This actual produces/sends out messages from the broker

Zookeeper - Manager of a kafka cluster, to help maintain it

- **Producers** write messages to topics (your factory simulator)
- **Consumers** read messages from topics (your analysis application)
- Messages are retained for a configured time period (retention policy)

1. Start Zookeeper first (manages the cluster)
2. Start Kafka broker(s) (handles the actual messages)
3. Create topics

***Creating setup***

```
version: '2'
services:
  zookeeper:
    image: confluentinc/cp-zookeeper:latest
    environment:
      ZOOKEEPER_CLIENT_PORT: 2181
      ZOOKEEPER_TICK_TIME: 2000
    ports:
      - "2181:2181"
  kafka:
    image: confluentinc/cp-kafka:latest
    depends_on:
      - zookeeper
    ports:
      - "9092:9092"
    environment:
      KAFKA_BROKER_ID: 1
      KAFKA_ZOOKEEPER_CONNECT: zookeeper:2181
      KAFKA_ADVERTISED_LISTENERS: PLAINTEXT://localhost:9092
      KAFKA_OFFSETS_TOPIC_REPLICATION_FACTOR: 1
```


So intialise zookeeper to then manage the later kafka as a client to which it connects to at `port: 2181` and kafka connects to via kafka_zookeeper_conenct

Used along side: `docker-compose up -d` to initialise tihs

***Creating new instance of a Producer:***

```
package main
import (
    "log"
    "time"
    "github.com/IBM/sarama"
)
func main() {
    config := sarama.NewConfig()
    config.Producer.Return.Successes = true
    producer, err := sarama.NewSyncProducer([]string{"localhost:9092"}, config)
    if err != nil {
        log.Fatalf("Error creating producer: %v", err)
    }
    defer producer.Close()
    for {
        sendMessage(producer)
        time.Sleep(1 * time.Second)
    }
}  

func sendMessage(producer sarama.SyncProducer) {
    msg := &sarama.ProducerMessage{
        Topic: "my-topic",
        Key:   sarama.StringEncoder("Key-1"),
        Value: sarama.StringEncoder("Hello Kafka with Sarama!"),
    }  
    partition, offset, err := producer.SendMessage(msg)
    if err != nil {
        log.Fatalf("Error sending message: %v", err)
    }
    log.Printf("Message is stored in partition %d, offset %d\n", partition, offset)
}
```

Producer sends a message to `my-topic`, and Kafka assigns to a partion and writes it to disk 


***Creating new instance of a Consumer:***

```
package main

import (
	"context"
	"log"
	"os"
	"os/signal"
	"sync"
	"github.com/IBM/sarama"
)

type Consumer struct {
	ready chan bool
}

func (consumer *Consumer) Setup(sarama.ConsumerGroupSession) error {
	close(consumer.ready)
	return nil
}

func (consumer *Consumer) Cleanup(sarama.ConsumerGroupSession) error {
	return nil
}

func (consumer *Consumer) ConsumeClaim(session sarama.ConsumerGroupSession, claim sarama.ConsumerGroupClaim) error {
	for message := range claim.Messages() {
		log.Printf("Message claimed: topic = %s, partition = %d, offset = %d, key = %s, value = %s",
			message.Topic, message.Partition, message.Offset, string(message.Key), string(message.Value))
		session.MarkMessage(message, "")
	}
	return nil
}

func main() {
	brokers := []string{"localhost:9092"}
	groupID := "my-group"
	topics := []string{"my-topic"}

	config := sarama.NewConfig()
	config.Version = sarama.V2_1_0_0
	config.Consumer.Group.Rebalance.Strategy = sarama.BalanceStrategyRoundRobin
	config.Consumer.Offsets.Initial = sarama.OffsetOldest
	consumer := Consumer{
		ready: make(chan bool),
	}
	client, err := sarama.NewConsumerGroup(brokers, groupID, config)
	if err != nil {
		log.Fatalf("Error creating consumer group client: %v", err)
	}
	defer client.Close()

	ctx, cancel := context.WithCancel(context.Background())
	wg := &sync.WaitGroup{}
	wg.Add(1)

	go func() {
		defer wg.Done()
		for {
			err := client.Consume(ctx, topics, &consumer)
			if err != nil {
				log.Fatalf("Error from consumer: %v", err)
			}
			if ctx.Err() != nil {
				return
			}
			consumer.ready = make(chan bool)
		}
	}()

	<-consumer.ready
	log.Println("Sarama consumer up and running... Press Ctrl+C to stop.")

	sigterm := make(chan os.Signal, 1)
	signal.Notify(sigterm, os.Interrupt)
	<-sigterm
	cancel()
	wg.Wait()
	log.Println("Consumer shut down cleanly")
}

```


Consumer subscribes to `my-topic` and reads messages from the partition logs, processing and marking them as consumed

***Reading from terminal***

``` shell

docker exec -it <name of kafka container> kafka-console-consumer --bootstrap-server localhost:9092 --topic <name of topic> --from-beginning

docker exec -it kafka kafka-console-consumer --bootstrap-server localhost:9092 --whitelist ".*"

```

##### References

----
