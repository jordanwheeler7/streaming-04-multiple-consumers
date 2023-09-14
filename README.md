# streaming-04-multiple-consumers
- [Jordan Wheeler](https://github.com/jordanwheeler7)
- CSIS 44671: Streaming Data
- 13 September 2023
- Module 4: Producer with Multiple Consumers
- [Repo Page](https://jordanwheeler7.github.io/streaming-04-multiple-consumers/)

## Assignment Description
This project is a continuation of the previous project. The goal is to use RabbitMQ to distribute tasks to multiple workers. One process will create task messages. Multiple worker processes will share the work.

## Requirements
- Virtual Environment
    -python3 -m venv .venv
    - Utilize .venv\Scripts\activate to start it
- Pika
    - pip install pika
    - python3 -m pip install pika
- RabbitMQ

## Instructions
> Use RabbitMQ to distribute tasks to multiple workers

One process will create task messages. Multiple worker processes will share the work. 


## Before You Begin

1. Fork this starter repo into your GitHub.
1. Clone your repo down to your machine.
1. View / Command Palette - then Python: Select Interpreter
1. Select your conda environment. 

## Read

1. Read the [RabbitMQ Tutorial - Work Queues](https://www.rabbitmq.com/tutorials/tutorial-two-python.html)
1. Read the code and comments in this repo.

## RabbitMQ Admin 

RabbitMQ comes with an admin panel. When you run the task emitter, reply y to open it. 

(Python makes it easy to open a web page - see the code to learn how.)

## Execute the Producer

1. Run emitter_of_tasks.py (say y to monitor RabbitMQ queues)

Explore the RabbitMQ website.

## Execute a Consumer / Worker

1. Run listening_worker.py

Will it terminate on its own? How do you know? 
- No, it will not terminate on its own. You can tell because the process is still running in the terminal. It all says to exit press CTRL+C.

## Ready for Work

1. Use your emitter_of_tasks to produce more task messages.

## Start Another Listening Worker 

1. Use your listening_worker.py script to launch a second worker. 

Follow the tutorial. 
Add multiple tasks (e.g. First message, Second message, etc.)
How are tasks distributed? 
Monitor the windows with at least two workers. 
Which worker gets which tasks?

## V3 - Multiple Workers Method
In v3, we utilized multiple workers to read a csv file. The first time we ran this, we used the standard that had 1-6 tasks. We then added additional tasks to this to see how our terminals would work. The tasks and more information are as follows:

1. Make a copy of v2 emitter and listening (this method is more commonly used in the field) and save them as v3.
2. We had to find a way to read in a csv file and then send the data to the queue. We did this by using the csv library and then using a for loop to send the data to the queue. Our inspiration came from the bonus project in [Module 3](https://github.com/jordanwheeler7/streaming-03-bonus-jordanwheeler).
3. We set our emitter to send a task every 2 seconds regardless of how long the task took to complete. We did this by using the time.sleep() function.
4. We created tasks in the csv file with varying (.) to see how the tasks would be picked up by our listening files. During periods that tasks were completed, the listening file would sleep until the emitter woke the file up again.
5. If we look at the screenshot below, you can see periods where one listener gathered 2 tasks consecutively while the other skipped tasks. This is because the listener was busy completing the task that it was given. This is a good example of how RabbitMQ can be used to distribute tasks to multiple workers.

## Reference

- [RabbitMQ Tutorial - Work Queues](https://www.rabbitmq.com/tutorials/tutorial-two-python.html)


## Screenshot

See a running example with at least 3 concurrent process windows here:
![P1](/P1.png)
