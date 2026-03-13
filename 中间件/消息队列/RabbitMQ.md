生产者   Producer
交换机   Exchange
队列      Queue
消费者   Consumer

1. **交换机**
	为什么需要交换机？
		解耦  不需要知道队列名字，队列数量，路由逻辑。生产者只需要知道交换机 + 路由key
		RabbitMQ 通过 Exchange 作为消息路由层，实现生产者和队列解耦，同时支持灵活的消息路由、一条消息分发到多个队列以及系统的动态扩展。
	交换机类型：
		1. Direct Exchange（直连交换）   routingKey = order.create   只会发送到绑定了 `order.create` 的队列
		2. Fanout Exchange（广播交换机）**不看 routingKey**   发送到 **所有绑定的队列**
		3.Topic Exchange（主题交换机）根据 **通配符匹配 routingKey**。


**RabbitMQ有哪些工作模式？**
1. 简单模式：点对点
2. 工作队列模式：一个生产者发送到队列中，多个消费者监听该队列。实现消息的负载均衡，常用于任务分发。
3. 发布/订阅模式：生产者将消息发送给广播交换机，Exchange 会把消息 **复制多份**。所有绑定交换机的都会受到消息
4. 路由模式：生产者将消息发送给直连交换机，不同路由键会受被分配到不同的队列，只订阅自己想要的
5. 主题交换机：主要是通配符
6. PRC模式，请求、相应双向通信
7. 发布确认模式：确保生产者消息发送的可靠性，适合确保消息到了的场景。


**如何确保消息不会丢失**
1. 消息持久化：确保队列和消息都是持久的，即使重启rabbitMQ也不会丢失
	```   msg：持久化队列
	channel.queue_declare(queue='task_queue', durable=True)
	```
	```  msg持久化消息
	channel.basic_publish(exchange='',
                      routing_key='task_queue',
                      body=message,
                      properties=pika.BasicProperties(
                         delivery_mode=2,  # make message persistent
                      ))

	```
2. 开启发布确认模式：这种模式下，生产者会等待服务器确认相应，确保消息能成功存储。
3. 消费者确认ack

**RabbitMQ死信队列**
RabbitMQ 本身支持 **Dead Letter Exchange（死信交换机）**。
1. 消息被拒绝
2. 消息过期TTL
3. 队列满了

**RabbitMQ没有原生的延迟队列**
TTL + 死信队列（最常见）
	订单消息 → 延迟队列(TTL=30分钟)
	消息过期 → 死信交换机
	进入 → 取消订单队列
延迟插件
