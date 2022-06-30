# Basic Terminology

## Learning Goals

- Explain critical sections, mutex, semaphore, and monitor.

## Critical Section

A critical section is any section of a code that has the possibility of being
executed concurrently by multiple threads and exposes any shared data used by
the process. A critical section should not be executed by multiple threads at
the same time.

Here’s the example from the previous lesson:

```java
class Counter {
    private int count = 0;

    public void increment() {
        count++;
    }

    public int getValue() {
        return count;
    }
}

class CountThread extends Thread {
    private final Counter counter;

    public CountThread(Counter counter) {
        this.counter = counter;
    }

    @Override
    public void run() {
        counter.increment();
    }
}

class Example {
    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();
        Thread t1 = new CountThread(counter);
        Thread t2 = new CountThread(counter);

        t1.start();
        t2.start();

        System.out.println(counter.getValue());
    }
}
```

The `count` variable is a critical section because multiple threads can perform
operations on it simultaneously.

## Mutex

A mutex (mutual exclusion) is a mechanism for guarding shared data. A mutex
allows only one thread to access data at a time. A thread acquires a mutex to
work on the data while all other threads have to wait for the first thread to
release the mutex before they can acquire the mutex.

A mutex that is locked by a thread must be unlocked by the same thread. A thread
has ownership of the mutex while it’s acquired.

## Semaphore

Semaphore is a way to limit access to resources. A semaphore has a limited
number of permits to give out to threads. Once it give all its permits to
threads any additional thread will be blocked from accessing the resource.

Semaphores don’t have the concept of ownership like mutexes. In the case of a
semaphore, different threads can call acquire and release on the semaphore.

## Monitor

A monitor is a mechanism for controlling concurrent access to an object.
Monitors are generally language level constructs whereas mutexes and semaphores
are lower-level constructs.

In Java, each object has an associated monitor that is hidden from the
developer. When a thread acquires a monitor other threads cannot acquire the
same monitor. The other threads has to wait for the first thread to release the
monitor before acquiring it.

## Conclusion

We’ve learned about the basic terms that come up in concurrency. In the next
lesson, we’ll learn how to manage access to shared dat.
