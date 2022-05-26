# Designing Data Intensive Applications

Nowadays most applications are data-intensive and typically offer similar functionalities:  they store info in databases, use caches for reads, search through indexes; and can handle stream processing, and batch processing. Unfortunately, systems have different end goals so applying a one size fits all approach to architecting just does not cut it. Understanding the important concerns with most software systems is a great place to start. These concerns are:
- [Reliability](#reliability)


### Reliability-
 continuing to work correctly, even when things go wrong.
a system is reliable if it:
- does what it is supposed to do.
- performs as expected even under load.
- is able to handle the user making mistakes.
- prevents unauthorised use

a fault tolerant system is able to spot and handle faults(the things that go wrong -- one component of the system deviating from its spec). faults and failure are not the same. Faults can be split into:
- hardware faults. caused by unresponsive hardware, these faults are pretty sporadic. RAID configuration for hard disks can help.
- software faults. can cause an avalanche of system failures, and are harder to anticipate. no quick solutions.
- human faults. leading cause of faults. good management practices, telemetry,a dn throrough tsting are good routes to ply.

Take reliability seriously. Think about how down-time/failures/faults can affect your business and users before deciding to cut corners.

Scalability - ability to cope with increased load
reliability is not fixed, increased load can cause degradation. Asking questions like “If the system grows in a particular way, what are our options for coping with the growth?” and “How can we add computing resources to handle the additional load?” can help put scalability into perspective, but first we must be able to accurately descibe our system's current load.

load parameters (how we describe load), again, can differ per system architecture. It can range anywhere from requests/s to the web server to db read/write ratios, tbh the opportunities are endless.
>> Describing load