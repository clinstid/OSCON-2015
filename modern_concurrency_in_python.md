# Plate Spinning: Modern Concurrency in Python
Plate spinning is a good analogy for concurrency because you can spin 18 plates at the same time with only two hands. Your hands are managing the plate spinning rather than doing the spinning itself. Concurrency is about managing multiple tasks running in parallel and making sure they all make progress.

# Generators
- Generator - any function that has a `yield` call.
- Caller sends values or generator yields values
- caller and generator progress is synchronized

# Spinner App
## Threaded
- Uses threading library
- Main thread runs the function that does the work
- Thread started to run a function that shows a spinner
- work function starts
- when it's done, sets `signal.go` to false which will stop the spinner thread
- main thread joins and returns the result

I/O or sleep function calls release the GIL allowing other Python bytecode to run. However, because of the GIL, CPU bound work will not run concurrently, so threading is not a concurrency option for CPU bound work.

## Coroutine yield/from
**Uses asyncio library**
- Main thread (only thread) starts event loop to drive coroutines
- `asyncio.ensure_future` (3.4.4) == `asyncio.async` (3.4.3)
- Use `asyncio.sleep` or else you will lose the CPU (if you use `time.sleep`)
- `yield from` is used to yield from another function - this breaks the lock stepped synchronization between the caller and the first function and blocks the generator function. Yields will be delegated to the `yield from` function - also known as the subgenerator.
- Tasks can be cancelled safely because asyncio tasks are single-threaded. Any task that is cancelled will raise a `asyncio.CancelledError` exception, so the function can do whatever clean up is required.
- asyncio has an event loop - `asyncio.get_event_loop`
- Using the event loop object, you call `run_until_complete` with the function to call.
- Coroutine functions are decorated with `@asyncio.coroutine`

The advantage of async tasks is that the async tasks use significantly less memory than multiple threads.

# My Thoughts
The coroutine/async method is interesting, but the threaded approach is much easier to understand. Perhaps the nomenclature clarifications in python 3.5 will make it easier to wrap your mind around the async methods.
