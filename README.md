# CopyService
University Project: asynchronous copy of files using a daemon in userspace (Linux); 

APIs included in my library:
- struct job CreateJob( const char* src, const char* dest);
-	void CancelJob();
- void PauseJob();
- void StartJob();
- void PrintJob();

The daemon is the server, which waits for orders (jobs) from multiple clients. 

These "clients" are test programs that send orders to the daemon using the library made available to us.

To succeed in communicating with the daemon, we use unix sockets, so it waits for commands from "clients" that connect in parallel to the socket.
For executing jobs we used the concept of thread pool, meaning that we have a limited number of threads (default in the config file for the daemon) that are in an infinite loop and are waiting for new jobs, which will be added in a queue.
On the synchronization side, the threads will be controlled by a mutex.
