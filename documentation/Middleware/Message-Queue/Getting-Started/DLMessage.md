# 死信队列

死信队列⽤于处理⽆法被正常消费的消息。当⼀条消息初次消费失败，消息队列会⾃动进⾏消息重试；达到最⼤重试次数后，若消费依然失败，则表明消费者在正常情况下⽆法正确地消费该消息，此时，消息队列不会⽴刻将消息丢弃，而是将其发送到该消费者对应的特殊队列中。将这种正常情况下⽆法被消费的消息称为死信消息（Dead-Letter Message），将存储死信消息的特殊队列称为死信队列（Dead-Letter Queue）。 

**应用场景**

**定位问题**：可以在死信队列中留出和隔离这些消息以确定其处理失败的原因，区分消息类型(普通、顺序)，可按照Topic和ConsumerGroup ID进行搜索。例如：某条消息被多次消费后却未被删除，一般是由于该消息未被正确消费，可能存在问题需要回溯定位。

您可以设置最大接收次数，超额后该消息会被淘汰到指定的死信队列，便于后续问题发现。

对于死信可以选择全部重新发送或者全部删除。全部重新发送，死信将再次进入topic发送给这条订阅关系的订阅者；全部删除，死信将全部删除，不再发送。到达死信队列上限后，topic会暂停发送消息功能，待用户处理订阅者的异常。
