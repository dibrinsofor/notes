# Designing Data Intensive Applications

nowadays most applications are data-intensive and typically offer similar functionalities:  they store info in databases, use caches to speed up reads, filter using indexes; and can handle stream and batch processing. Unfortunately, systems have different end goals so applying a one size fits all approach to architecting just does not cut it. Understanding the important concerns with most software systems is a great place to start. These concerns are:
- [reliability](#reliability-)
- [scalability](#scalability-)
- [maintainability](#maintainability-)

## **Reliability-**
>continuing to work correctly, even when things go wrong.

a system is reliable if it:

- does what it is supposed to do.

- performs as expected even under load.

- is able to handle the user making mistakes.

- prevents unauthorised use

a *fault tolerant* system is able to spot and handle faults -- the things that go wrong or one component of the system deviating from its spec. faults and failure are not the same. Faults can be split into:

- hardware faults. caused by unresponsive hardware, these faults are pretty sporadic. RAID configuration for hard disks can help.

- software faults. can cause an avalanche of system failures, and are harder to anticipate. no quick solutions.

- human faults. the leading cause of faults. good management practices, telemetry and throrough testing are good routes to ply.

take reliability seriously. Think about how down-time/failures/faults can affect your business and users before deciding to cut corners.

## **Scalability-** 
>ability to cope with increased load.

reliability is not constant, increased load can cause degradation. Asking questions like “If the system grows in a particular way, what are our options for coping with the growth?” and “How can we add computing resources to handle the additional load?” can help put scalability into perspective, but first we must be able to accurately descibe our system's current load.

load parameters (how we describe load), again, can differ per system architecture. It can range anywhere from server requests/sec to database read/write ratios, tbh the opportunities are endless.

in the case of Twitter, a service whose primary functions are to post tweets and view timelines, even while handling over 12k requests/sec at peak times in 2012, their scalability challenge was not because of tweet volume but due to *fan-out* -- placing a user's tweet into their followers' timelines.

>fan-out is the process of delivering a message to one or multiple destinations possibly in parallel, and not halting the process that executes the messaging to wait for any response to that message.

to fix this they decided to cache each user's home timeline. This way when a tweet is sent out the service looks up all the users who follow the tweet's sender and inserts this tweet into their respective caches. Adopting just this approach may not work as efficiently for users with millions of followers as writes to follower's timelines become too expensive. Twitter now adopts a hybrid fan-out system that leverages caches for average use cases and index searching for the more expensive cases. 

once we're able to describe our system's load then we can start to look into what happens when said load increases (system performance). We can ask these questions: how will increased load affect performance if we keep our system resources the same? and how much do we need to increase our resources to keep performance the same if load increases?

in online systems we are typically more interested in *response time* rather than *throughput*. 
>throughput is the number of records we can process per second, or the total time it takes to run a job on a dataset of a certain size.

>response time vs latency? Latency is the duration that a
request is waiting to be handled—during which it is awaiting service while response time is the time between a client sending and recieving a response, including network and queueing delays.

the median (p50 or 50th percentile) --using percentiles-- helps paint a more accurate picture of system performance than the mean (average) does. If your median response time is 200 ms, that means half your requests return in less than 200 ms, and half your requests take longer than that. The median is a good metric to measure how long users have to wait to get responses. 

*tail latencies* (high percentiles of response times) directly affect users' experience, optimizing for the users in the 99th percentile may prove beneficial as these users have the most amount of data on thier accounts. on the other hand, optimizing the 99.99th percentile of requests may not be as cost effective. 

*queueing delays* play a huge role in increasing response times for the high percentiles. one or two of these slow requests can hold up future requests -- *head-of-line blocking*. 
> measuring response times on the client side is necessary because of this.

having understood load parameters and optimal metrics for measuring system performance, the next logical question is "how do we maintain good performance even when our load parameters increase by some amount?"

you may need to rethink your architecture on every order of magnitude load increase.

>horizontal scaling vs vertical scaling? horizontal scaling (shared-nothing architecture) involves distributing load across multiple machines. Vertical scaling involves moving the system to a more powerful machine to handle processing.

tbh, good architecture usually involves a mixture of both approaches. Also, when load is unpredictable consider an elastic system (a system that automatically detects load increases and adds computing resources). To reduce additional complexity, keep your database on a single-node until the system forces you distribute it.

## **Maintainability-**

a major part of the cost of software is in maintenance.

we can and should design software in such a way that it will hopefully minimize pain during maintenance, and thus avoid creating legacy software ourselves.

three design principles to take note of:

- operability:

        make it easy for operations teams to keep the system running smoothly.

- simplicity:

        make it easy for new engineers to understand the system, by removing as much complexity as possible from the system. not related to UI.

- evolvability:

        make it easy for engineers to make changes to the system in the future, adapting it for unanticipated use cases as requirements change.

taking these principles into account when architecting systems is necessary and may improve maintainability.