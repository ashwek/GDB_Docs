# 7 Recording Inferior’s Execution and Replaying It

----

On some platforms, GDB provides a special process record and replay target that can record a log of the process execution, and replay it later with both forward and reverse execution commands.

_When this target is in use, if the execution log includes the record for the next instruction, GDB will debug in replay mode. In the replay mode, the inferior does not really execute code instructions. Instead, all the events that normally happen during code execution are taken from the execution log. While code is not really executed in replay mode, the values of registers (including the program counter register) and the memory of the inferior are still changed as they normally would. Their contents are taken from the execution log._

If the record for the next instruction is not in the execution log, GDB will debug in record mode. In this mode, the inferior executes normally, and GDB records the execution log for future replay.

The process record and replay target supports reverse execution, even if the platform on which the inferior runs does not. However, the reverse execution is limited in this case by the range of the instructions recorded in the execution log. In other words, reverse execution on platforms that don’t support it directly can only be done in the replay mode.

When debugging in the reverse direction, GDB will work in replay mode as long as the execution log includes the record for the previous instruction; otherwise, it will work in record mode, if the platform supports reverse execution, or stop if not.

For architecture environments that support process record and replay, GDB provides the following commands:

```
record method
```
This command starts the process record and replay target. The recording _method_ can be specified as parameter. Without a parameter the command uses the full recording method. The following recording methods are available:

```
record full
```
Full record/replay recording using GDB’s software record and replay implementation. This method allows replaying and reverse execution.

```
record btrace format
```
Hardware-supported instruction recording, supported on Intel processors. This method does not record data. Further, the data is collected in a ring buffer so old data will be overwritten when the buffer is full. It allows limited reverse execution. Variables and registers are not available during reverse execution.

The recording _format_ can be specified as parameter. Without a parameter the command chooses the recording format. The following recording formats are available:

```
record btrace bts
```
Use the Branch Trace Store (BTS) recording format. In this format, the processor stores a from/to record for each executed branch in the btrace ring buffer.

```
record btrace pt
```
Use the Intel Processor Trace recording format. In this format, the processor stores the execution trace in a compressed form that is afterwards decoded by GDB.

Decoding the recorded execution trace, on the other hand, is more expensive than decoding BTS trace. This is mostly due to the increased number of instructions to process. You should increase the buffer-size with care.

Not all recording formats may be available on all processors.

The process record and replay target can only debug a process that is already running. Therefore, you need first to start the process with the run or start commands, and then start the recording with the record method command.

Displaced stepping will be automatically disabled when process record and replay target is started. That’s because the process record and replay target doesn’t support displaced stepping.

If the inferior is in the non-stop mode or in the asynchronous execution mode, not all recording methods are available. The full recording method does not support these two modes.

```
record stop
```
Stop the process record and replay target. When process record and replay target stops, the entire execution log will be deleted and the inferior will either be terminated, or will remain in its final state.

When you stop the process record and replay target in record mode (at the end of the execution log), the inferior will be stopped at the next instruction that would have been recorded. In other words, if you record for a while and then stop recording, the inferior process will be left in the same state as if the recording never happened.

On the other hand, if the process record and replay target is stopped while in replay mode (that is, not at the end of the execution log, but at some earlier point), the inferior process will become “live” at that earlier state, and it will then be possible to continue the usual “live” debugging of the process from that state.

When the inferior process exits, or GDB detaches from it, process record and replay target will automatically stop itself.

```
record goto
```
Go to a specific location in the execution log. There are several ways to specify the location to go to:

```
record goto begin
record goto start
```
Go to the beginning of the execution log.

```
    record goto end
```
Go to the end of the execution log.

```
    record goto n
```
Go to instruction number n in the execution log.

```
record save filename
```
Save the execution log to a file _filename_. Default filename is gdb_record.process_id, where process_id is the process ID of the inferior.


This command may not be available for all recording methods.
```
record restore filename
```
Restore the execution log from a file filename. File must have been created with record save.

```
set record full insn-number-max limit
set record full insn-number-max unlimited
```
Set the limit of instructions to be recorded for the full recording method. Default value is 200000.

```
show record full insn-number-max
```
Show the limit of instructions to be recorded with the full recording method.

```
set record full stop-at-limit
```
Control the behavior of the full recording method when the number of recorded instructions reaches the limit. If ON (the default), GDB will stop when the limit is reached for the first time and ask you whether you want to stop the inferior or continue running it and recording the execution log. If you decide to continue recording, each new recorded instruction will cause the oldest one to be deleted.

If this option is OFF, GDB will automatically delete the oldest record to make room for each new one, without asking.

```
show record full stop-at-limit
```
Show the current setting of stop-at-limit.

```
set record full memory-query
```
Control the behavior when GDB is unable to record memory changes caused by an instruction for the full recording method. If ON, GDB will query whether to stop the inferior in that case.

If this option is OFF (the default), GDB will automatically ignore the effect of such instructions on memory. Later, when GDB replays this execution log, it will mark the log of this instruction as not accessible, and it will not affect the replay results.

```
show record full memory-query
```
Show the current setting of memory-query.

```
info record
```
Show various statistics about the recording depending on the recording method:

```
record delete
```
When record target runs in replay mode (“in the past”), delete the subsequent execution log and begin to record a new execution log starting from the current address. This means you will abandon the previously recorded “future” and begin recording a new “future”.

```
record instruction-history
```
Disassembles instructions from the recorded execution log. By default, ten instructions are disassembled. This can be changed using the set record instruction-history-size command. Instructions are printed in execution order.
