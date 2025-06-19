# Service Bus CheatSheet
* * * 

## ✅ Positive Tests

1. Basic message delivery

Given a message producer is connected to the Service Bus queue <br>
When a valid message is sent to the queue <br>
Then the message should be received by the consumer <br>
And the message content should be processed successfully <br>


2. Multiple messages in sequence

Given the queue is empty <br>
When 5 valid messages are sent to the queue in sequence <br>
Then all 5 messages should be received by the consumer in the order they were sent <br>


3. Message with specific properties (e.g., correlation ID)

Given a message with a correlation ID is sent to the queue <br>
When the consumer receives the message <br>
Then the consumer should log the correlation ID <br>
And process the message without errors <br>

4. Message with delay (Scheduled Message)

Given a message is scheduled to be sent to the queue 30 seconds in the future <br>
When 30 seconds have passed <br>
Then the consumer should receive and process the message <br>


## ❌ Negative Test Scenarios

5. Invalid message schema

Given a message with an invalid schema is sent to the queue <br>
When the consumer attempts to process the message <br>
Then the consumer should log a validation error <br>
And move the message to the dead-letter queue <br>

6. Expired TTL (Time to Live)

Given a message is sent with a TTL of 5 seconds <br>
When the message is not consumed within 5 seconds <br>
Then the message should expire <br>
And the message should not be delivered to the consumer <br>

7. Unreachable Service Bus

Given the Service Bus is unreachable due to a network issue <br>
When the producer tries to send a message <br>
Then the message should not be sent <br>
And an error should be logged by the producer <br>

8. Consumer throws unhandled exception

Given a valid message is sent to the queue <br>
When the consumer throws an unhandled exception while processing <br>
Then the message should be retried up to the max delivery count <br>
And then moved to the dead-letter queue <br>

9. Unauthorized sender

Given a sender with invalid credentials attempts to send a message <br>
When the message is submitted <br>
Then the message should be rejected <br>
And the attempt should be logged as unauthorized <br>

* * *
