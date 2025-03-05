# SQS-SNS-EventBridge
SQS-SNS-EventBridge Knowledge Hub

   
1. Does SNS guarantee exactly-once delivery to subscribers?   
No, Amazon SNS does not guarantee exactly-once delivery. While SNS ensures at least once delivery (meaning messages will be delivered to subscribers, but there may be retries in case of failure), it does not guarantee that each message is delivered only once. The system is designed to retry delivery in case of transient failures, and there is a possibility of message duplication under certain conditions (such as network issues or subscriber unavailability).
If your application requires exactly-once processing, you will need to handle de-duplication on the subscriber side, either by storing a unique identifier with each message or using a deduplication mechanism.   


   
3. What is the purpose of the Dead-letter Queue (DLQ)?   
A Dead-letter Queue (DLQ) is a feature that allows you to capture and store messages that couldn’t be processed successfully by the consumer or subscriber. This is useful for troubleshooting and debugging issues when messages fail to be delivered or processed.
Purpose of DLQ:
Error Handling: When messages cannot be successfully delivered or processed, they are sent to the DLQ after a predefined number of delivery attempts or processing failures.   
Message Retention: DLQs allow you to retain these failed messages for further investigation, analysis, or later processing.   
Monitoring: DLQs can be used to track errors in the message delivery process and monitor the health of your systems.   
DLQs are available for several AWS services, including SNS, SQS, and EventBridge.   

      
5. How would you enable a notification to your email when messages are added to the DLQ?     
To enable a notification to your email when messages are added to a Dead-letter Queue (DLQ), you can use Amazon CloudWatch Alarms in combination with SNS. The steps are as follows:   
Step-by-step process:   
Create an SNS Topic for Notifications:
Go to the SNS Console.   
Create a new SNS topic that will be used for notifications.   
Subscribe your email address to the SNS topic.      
Create a CloudWatch Alarm for DLQ:   
Navigate to the CloudWatch Console.    
Go to Alarms and click Create Alarm.    
For the metric, select the DLQ's metrics (you can find these under SQS metrics or SNS metrics, depending on your use case).   
For SNS, you'd look for metrics like NumberOfMessagesSent or NumberOfMessagesInDeadLetterQueue.   
Set the condition for the alarm to trigger when a certain threshold of messages appears in the DLQ (for example, if the number of messages in the DLQ exceeds 0).   
Set SNS as the Alarm Action:   
In the alarm setup, specify the SNS topic you created in Step 1 as the action to take when the alarm state is triggered.   
This will send a notification to your email whenever the DLQ receives messages.   
Test the Setup:   
Send some messages to the service (SNS, SQS, EventBridge) that may end up in the DLQ, and verify that you receive an email notification when they are added to the DLQ.   
By following these steps, you'll get an email notification whenever a message ends up in the DLQ, helping you monitor and address issues more effectively.    
   

