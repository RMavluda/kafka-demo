# Kafka Demo with Spring Boot

A simple **Spring Boot Kafka demo project** used to learn and test **Apache Kafka consumer functionality** before integrating Kafka into a real CRUD application.

This project focuses on:
- Kafka setup with Docker (Kafka + ZooKeeper)
- Kafka consumer configuration
- Consuming messages from a Kafka topic using Spring Kafka

---

## 🚀 Features
- Kafka Consumer using `@KafkaListener`
- Kafka + ZooKeeper via Docker Compose
- Simple message consumption from Kafka topic
- Java 17 & Spring Boot–based setup
- Clean separation from main business application

---

## 🛠 Tech Stack
- Java 17
- Spring Boot
- Spring Kafka
- Apache Kafka
- ZooKeeper
- Docker & Docker Compose
- Maven

---

## 🧱 Architecture Overview

```

┌──────────────────┐
│ Kafka Producer   │
│ (External App)   │
│ (CRUD Project)  │
└─────────┬────────┘
│
│ Kafka Message
▼
┌──────────────────┐
│ Kafka Broker     │
│  Topic: course   │
└─────────┬────────┘
│
▼
┌──────────────────┐
│ KafkaConsumer    │
│ (@KafkaListener) │
│ Spring Boot App  │
└──────────────────┘

```

This project **only consumes messages**.  
Message production is handled by another application (e.g. the Consumer CRUD project).

---

## 📂 Project Structure
```

src
└── main
└── java
└── com.example.demo.kafka
└── KafkaConsumer.java

````

---

## 🐳 Kafka & ZooKeeper Setup (Docker)

Start Kafka and ZooKeeper using Docker Compose:

```bash
docker compose up -d
````

### Services

* ZooKeeper: `localhost:2181`
* Kafka Broker: `localhost:9092`

Kafka runs with a single broker and is suitable for local development/testing.

---

## ▶️ Run the Application

```bash
./mvnw spring-boot:run
```

Once running, the application will listen to Kafka messages.

---

## 🧾 Kafka Consumer

Kafka consumer listens to topic `course`:

```java
@KafkaListener(topics = "course", groupId = "my_consumer")
public void listen(String message) {
    System.out.println("Received: " + message);
}
```

When a message is published to the topic, it will be printed in the console.

---

## 🧪 How to Test

1. Start Kafka & ZooKeeper:

```bash
docker compose up -d
```

2. Run this Spring Boot application.

3. Send messages using:

   * Kafka console producer
   * Or another Spring Boot project acting as Kafka Producer

Example using Kafka CLI:

```bash
docker exec -it kafka kafka-console-producer \
  --topic course \
  --bootstrap-server localhost:9092
```

Type a message and press enter:

```
Hello Kafka
```

Application output:

```
Received: Hello Kafka
```

---

## 🎯 Purpose of This Project

This project is created as a **learning and testing environment** to:

* Understand Kafka fundamentals
* Test Kafka configuration
* Validate consumer logic

After validation, Kafka functionality was integrated into the main **Spring Boot Consumer CRUD project**.

---

## 🔮 Possible Enhancements

* Add Kafka Producer to this project
* Consume structured (JSON) messages
* Error handling & retry mechanism
* Dead Letter Topic (DLT)
* Logging & metrics

---

## 👩‍💻 Author

**Mavluda Raximquliyeva**

---

## 📝 Notes

* Kafka broker must be running before starting the application
* This project is intentionally kept simple for learning purposes

````
