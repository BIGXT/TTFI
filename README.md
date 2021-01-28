# TTFI
 Fault diagnosis experiments with the TrainTicket application.

## Basis:

*Experimental Applications：[TrainTicket](https://github.com/FudanSELab/train-ticket)

*Chaos Engineering: [Chaosblade](https://github.com/chaosblade-io/chaosblade#chaosblade-an-easy-to-use-and-powerful-chaos-engineering-toolkit)

## Experimental use cases

The following table shows the fault injection experiments we conducted：

| Injecting Faulty Objects | Fault numbers | Root causes | Details |
| ------ | ------ | ------ | ------ |
| TrainTicket Application | F1 | OOM errors of JVM. | Causes the application's heap memory footprint to exceed the Xmx limit, triggering an overflow. |
|  | F1 | OOM errors of JVM. | Causes the application's heap memory footprint to exceed the Xmx limit, triggering an overflow. |
|  | F2 | Network communication delayed between microservices. | Make the communication of ts-cancel-microservice incur a 200ms delay and timeout for partially sent cancellation requests. |
|  | F3 | Network communication lost and generates unexpected errors. | Make the communication of ts-travel2-microservice generate 70% packet loss, and some requests to send notifications are lost. |
|  | F4 | The microservice was accidentally deleted. | Delete the pod: ts-admin-user-microservice, which is used to provide user management operations. |
|  | F5 | The CPU of the Java process in the container is fully loaded. | CPU full for java process in ts-admin-route-microservice service container. |
|  | F6 | Unexpected increase in processing time for some requests due to latency in the method. | The createNewOrder method in the java process of the ts-order-microservice service injects 3s fault, which controls the generation of new orders. |
| Containers | F7 | Triggers an error hang of the microservice container, resulting in unexpected errors in business processing.	| Hang the container of ts-notification-microservice. |
|  |F8 | The CPU load in the container is 100%. | Increase the pod’s CPU load of ts-config-microservice |