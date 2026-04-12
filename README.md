# compx234readers-writers-lab2
This program implements a **pipe-style** reader-writer synchronization scheme using Python threads and the threading.Condition class. It follows the following core rules:
1. When there are no writers, multiple readers can simultaneously access the shared resource.
2. Writers must have exclusive access. At any given time, only one writer can be active, and writers and readers cannot run concurrently.
3. A safe waiting/waking mechanism is used. After being awakened, the thread will recheck the condition to avoid concurrent errors.

ReaderWriterMonitor class: Uniformly controls access to shared resources
Shared Counter:
active_readers: The current number of readers who are reading
active_writers: Whether there is a writer currently writing (0 or 1)
waiting_writers: The current number of writers waiting
Synchronization Mechanism: Implemented using Condition to handle waiting (wait) and waking up (notify_all) 

1. When the reader starts reading: Wait until there are no writers, then increment the reader count by 1.
2. When the reader finishes reading: Decrement the reader count by 1. If it is the last reader, wake up the waiting thread.
3. When the writer starts writing: Wait until there are no readers and no writers, then acquire the exclusive resource.
4. When the writer finishes writing: Release the exclusive access, and wake up all waiting threads.

PS C:\Users\Lenovo\Desktop\A2> & C:/Users/Lenovo/AppData/Local/Python/pythoncore-3.14-64/python.exe c:/Users/Lenovo/Desktop/A2/readers_writers_starter.py
Reader 2 wants to read
📖 Reader 2 starts reading | Active readers:1
Reader 2 is READING
Reader 3 wants to read
📖 Reader 3 starts reading | Active readers:2
Reader 3 is READING
Writer 1 wants to write
Reader 1 wants to read
📖 Reader 1 starts reading | Active readers:3
Reader 1 is READING
Writer 2 wants to write
📕 Reader 2 ends reading   | Active readers: 2
Reader 2 finished reading
📕 Reader 1 ends reading   | Active readers: 1
Reader 1 finished reading
Reader 1 wants to read
📖 Reader 1 starts reading | Active readers:2
Reader 1 is READING
📕 Reader 3 ends reading   | Active readers: 1
Reader 3 finished reading
Reader 2 wants to read
📖 Reader 2 starts reading | Active readers:2
Reader 2 is READING
📕 Reader 1 ends reading   | Active readers: 1
Reader 1 finished reading
Reader 3 wants to read
📖 Reader 3 starts reading | Active readers:2
Reader 3 is READING
📕 Reader 2 ends reading   | Active readers: 1
Reader 2 finished reading
Reader 1 wants to read
📖 Reader 1 starts reading | Active readers:2
Reader 1 is READING
Reader 2 wants to read
📖 Reader 2 starts reading | Active readers:3
Reader 2 is READING
📕 Reader 1 ends reading   | Active readers: 2
Reader 1 finished reading
📕 Reader 3 ends reading   | Active readers: 1
Reader 3 finished reading
📕 Reader 2 ends reading   | Active readers: 0
Reader 2 finished reading
✏️  Writer 1 starts writing  | Waiting writers: 1
Writer 1 is WRITING
Reader 3 wants to read
🖊️  Writer 1 ends writing
Writer 1 finished writing
📖 Reader 3 starts reading | Active readers:1
Reader 3 is READING
📕 Reader 3 ends reading   | Active readers: 0
Reader 3 finished reading
✏️  Writer 2 starts writing  | Waiting writers: 0
Writer 2 is WRITING
Writer 1 wants to write
🖊️  Writer 2 ends writing
Writer 2 finished writing
✏️  Writer 1 starts writing  | Waiting writers: 0
Writer 1 is WRITING
Writer 2 wants to write
🖊️  Writer 1 ends writing
Writer 1 finished writing
✏️  Writer 2 starts writing  | Waiting writers: 0
Writer 2 is WRITING
🖊️  Writer 2 ends writing
Writer 2 finished writing
