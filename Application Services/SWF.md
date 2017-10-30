# Simple Workflow Service

![Alt_Text](https://image.slidesharecdn.com/svc201-131119165136-phpapp02/95/automate-your-big-data-workflows-svc201-aws-reinvent-2013-3-638.jpg?cb=1434517835 "SWF")
* Fully  managed workflow service provided by AWS
* **workflow** allows an architect/developer to implement distributed, asynchronous application asn a workflow
* **workflow** coordinates and manages the execution of activiities that an be run asynchronously across multiple computing devices
* SWF has consistent execution
* Gurantees the order in which tasks are executed
* There are no duplicate tasks
* The SWF service is primarily an API which application can integrate its work flow service into. 
This allows the service to be used by non-AWS services, such as on-premise data center
* A workflow execution can last upto 1 year

## Components of SWF
* **Workflow** : A sequence of steps required to perform a specific task
  * A workflow is also commonly referred as **decider**
* **Acitivites** : A single step (or unit of work) in the workflow
* **Tasks** : What Interacts with the "workers" taht are part of workflow.
    * Activity Task: Tells the worker tp erform a funtion
    * Decision task - tells the decider the state of the work flow execution, which allows the 
    decider to determine the next activity to be performend
    * Worker: Responsible for receiving a task and taking action on it.
          * an be any type of component such as an EC2 instance, or even a person

