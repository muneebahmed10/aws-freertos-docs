# coreMQTT library<a name="freertos-lib-coremqtt-agent"></a>

## Introduction<a name="coremqtt-agent-introduction"></a>

The coreMQTT Agent library is a high level API that adds thread safety to the [coreMQTT]() library\. It lets you create a dedicated MQTT agent task that manages an MQTT connection in the background and doesn't need any intervention from other tasks\. The library provides thread safe equivalents to the coreMQTT's APIs, so it can be used in multi-threaded environments\.

The MQTT agent is an independent task (or thread of execution)\. It achieves thread safety by being the only task that is permitted to access the MQTT library's API\. It serializes access by isolating all MQTT API calls to a single task, and it removes the need for semaphores or any other synchronization primitives\.

The library uses a thread safe messaging queue (or other inter-process communication mechanism) to serialize all requests to call MQTT APIs\. The messaging implementation is decoupled from the library through a messaging interface, which allows the library to be ported to other operating systems\. The messaging interface is composed of functions to send and receive pointers to the agent's command structures, and functions to allocate these command objects, which allows the application writer to decide the memory allocation strategy appropriate for their application\.

The library is written in **C** and designed to be compliant with [ISO C90](https://en.wikipedia.org/wiki/ANSI_C#C90) and [MISRA C:2012](https://www.misra.org.uk/MISRAHome/MISRAC2012/tabid/196/Default.aspx)\. The library has no dependencies on any additional libraries other than coreMQTT and the standard C library\. The library has [proofs](https://www.cprover.org/cbmc/) that show safe memory use and no heap allocation, so it can be used for IoT microcontrollers, but is also fully portable to other platforms\. It can be freely used, and is distributed under the [MIT open source license](https://freertos.org/a00114.html)\.

When using MQTT connections in IoT applications, we recommended that you use a secure transport interface, such as one that uses the TLS protocol\.

This MQTT library doesn't have platform dependencies, such as threading or synchronization\. This library does have [proofs](https://www.cprover.org/cbmc/) that demonstrate safe memory use and no heap allocation, which makes it suitable for IoT microcontrollers, but also fully portable to other platforms\. It can be freely used, and is distributed under the [MIT open source license](https://freertos.org/a00114.html)\.


****  

| Code Size of coreMQTT Agent \(example generated with GCC for ARM Cortex\-M\) | File | With \-O1 Optimisation | With \-Os Optimisation | 
| --- | --- | --- | --- | 
| core\_mqtt_agent\.c | 1\.7K | 1\.5K | 
| core\_mqtt_agent_command_functions\.c | 0\.3K | 0\.2K | 
| core\_mqtt\.c | 3\.0K | 2\.6K | 
| core\_mqtt\_state\.c | 1\.4K | 1\.1K | 
| core\_mqtt\_serializer\.c | 2\.5K | 2\.0K | 
| Total estimate | 8\.9K | 7\.4K | 
