# Systems, Kernels, And Unsafe Code Overlay

Use this overlay for operating systems, kernels, drivers, firmware, runtimes, embedded systems, unsafe code, low-level concurrency, ABI boundaries, or hardware-near software.

## Applicability

This overlay applies when work touches:

- OS or kernel code,
- drivers or firmware,
- boot or recovery paths,
- unsafe memory operations,
- FFI boundaries,
- memory allocators,
- schedulers,
- concurrency primitives,
- architecture-specific code,
- low-level runtime internals.

## ABI/API Compatibility

Before changing an interface, identify:

- consumers,
- documented behavior,
- binary compatibility,
- source compatibility,
- syscall/ioctl/protocol contracts,
- structure layout,
- alignment,
- endianness,
- migration path.

Use `.agent/TEMPLATES/INTERFACE_CONTRACT.md` where useful.

## Unsafe Code And Undefined Behavior

Review:

- pointer aliasing,
- lifetimes,
- bounds,
- initialization,
- alignment,
- integer overflow,
- object ownership,
- FFI safety,
- undefined behavior,
- compiler assumptions.

Unsafe code should have local invariants documented near the code or in a design note.

## Concurrency And Interrupts

Consider:

- races,
- deadlocks,
- preemption,
- interrupt context,
- signal context,
- lock ordering,
- priority inversion,
- cancellation,
- resource cleanup,
- memory ordering,
- synchronization,
- atomicity.

## Resource Lifetime

Track ownership and lifetime for:

- memory,
- file descriptors,
- handles,
- locks,
- DMA buffers,
- hardware queues,
- interrupts,
- timers,
- threads,
- tasks.

## Validation

Consider:

- unit tests,
- integration tests,
- kernel selftests,
- fault injection,
- fuzzing,
- static analysis,
- dynamic analysis,
- sanitizers,
- model checking,
- cross-platform tests,
- architecture-specific tests,
- boot and recovery tests.

## Rollback And Recovery

High-risk systems changes should identify:

- feature flag or disable path,
- previous known-good version,
- recovery media or boot path,
- data corruption risk,
- telemetry needed to diagnose failure,
- field rollback constraints.

## Specialist Review

Request systems/kernel/unsafe/firmware review when work changes ABI/API boundaries, unsafe code, concurrency, memory ordering, hardware interaction, boot paths, or recovery behavior.
