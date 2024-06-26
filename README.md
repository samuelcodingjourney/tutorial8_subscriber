### Tutorial 8
a. what is amqp?
AMQP stands for Advanced Message Queuing Protocol. Basically it is a messaging protocol for systems in order to be able to communicate asynchronously via message queues. 

b. what it means? guest:guest@localhost:5672 , what is the first guest, and what is the second guest, and what is localhost:5672 for?
For the url guest:guest@localhost:5672, in here first guest is username. Second guest is password. Lastly, localhost:5672 is the address and port of server. So the server should be running on the same machine because of localhost usage here and listening on port 5672.

Simulation slow subscriber:
![Screenshot (1058)](https://github.com/samuelcodingjourney/tutorial8_subscriber/assets/94734973/80648374-16c2-41fb-995a-b79adebeda85)

![Screenshot (1063)](https://github.com/samuelcodingjourney/tutorial8_subscriber/assets/94734973/9b4ef94a-25da-4f8d-af5d-5b06239d784d)

Total number of queues in my machine is 21 because in the subscriber program there is a delay of one second for every message processing. Uncommenting thread::sleep(ten_millis) would introduce delay of one second for every message processing. So the subscriber processing is slower than the publisher message production rate. This would result in a backlog of messages being accumulated in the message queue. Because the message queue is overwhelmed, RabbitMQ would dynamically create another queue to accomodate increased demand. This is why my total number of queues is 21 instead of 20. 

Reflection and Running at least three subscribers:
![Screenshot (1064)](https://github.com/samuelcodingjourney/tutorial8_subscriber/assets/94734973/bb5c99d5-dde2-4081-a0bc-9cdf93815b8e)

![Screenshot (1070)](https://github.com/samuelcodingjourney/tutorial8_subscriber/assets/94734973/7dc93ab5-b2c9-454c-af05-89af522bb7e7)

The number of queues is now 13 when running cargo run 7 times on the publisher program with three subscribers instances running instead of the previously 21. This is because now there are three subscribers that are processing the message together. This means that the subscriber instances are being run concurrently, so that the event processing task is split between them. The workload will be distributed and so speed up the message consumption as can be seen from the above screenshot graph different from only having one subscriber. 

Ways to imrpove both codes of publisher and subscriber is that by using techniques such as paralleilsm or thread pools. Load balancing is also needed because now multiple subscriber instances can be created. Other fault tolerance mechanisms in order to handle failures in the subscriber instances are needed and features such as automatic recovery, retry mechanisms, or other message reprocessing techniques could ensure a more reliable message consumption by the subscribers even when faced with failures.
