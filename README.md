# Publisher

## a. How much data will the publisher send to the message broker in a single execution?

In its current implementation, the publisher transmits exactly three distinct messages during a single run. Each message encapsulates a UserCreatedEventMessage object, which consists of two string fields: a user_id and a user_name. Consequently, every time you execute `cargo run`, the broker receives three event payloads destined for the "user_created" queue.

## b. What is the significance of using the identical URL in both the subscriber and publisher?

The consistency of the URL (`amqp://guest:guest@localhost:5672`) is fundamental to the system's architecture. It signifies that both components are converging on the same message broker instance to facilitate communication. Since the publisher and subscriber are decoupled, they rely on this shared "meeting point" to ensure that the messages dispatched by one are successfully intercepted and processed by the other. If these addresses differed, the publisher would be broadcasting to a void, and the subscriber would be listening to a different, potentially empty, channel.

![RabbitMQ](image.png)