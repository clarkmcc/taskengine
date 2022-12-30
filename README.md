# taskengine
An extensible Go task scheduler and executor. I've been working on several iterations of a task engine and am finally getting to the point where we've figured out what works, and what doesn't work. The use-case of the task engine is mainly for IoT applications, where agents are not neccesarily within our control, but we want to be able to run operations on a schedule, or send commands to the agents, and let the agents run those commands immediately.

## Design Goals
* Register named tasks that support arbitrary payloads.
* Tasks can be scheduled using several scheduling methodolgies like cron, interval, adhoc, once, etc.
* Tasks can be called just like functions.
* Specify which types of tasks are allowed to run concurrently with eachother.
* Execute more than one task at a time by using a job. This is helpful for when one task depends on another task and must run sequentially with other tasks.
* Supports task cancellation via a propagated context.
* Supports a context type that's generic over `T`, where `T` is any type that you provide. This allows you to plumb anything you wany from the task engine, into the tasks themselves.
* Supports the [slog](https://pkg.go.dev/golang.org/x/exp/slog) logger with an optional log sink so that you can capture logs emitted by your tasks and push them somewhere else.
