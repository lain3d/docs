---
description: Description of '?' command in HyperDbg.
---

# ? \(evaluate and execute expressions and scripts in debuggee\)

### Command <a id="command"></a>

> ?

### Syntax <a id="syntax"></a>

> ? \[expression\]

### Description <a id="description"></a>

Evaluates and executes an expression in the remote debuggee.

### Parameters <a id="parameters"></a>

**\[expression\]**

The expression is based on HyperDbg's [scripting language](https://web.archive.org/web/20210228003007/https://docs.hyperdbg.org/commands/scripting-language/assumptions-and-evaluations).

### Examples <a id="examples"></a>

The following command shows the `@rax` register in the debuggee by calling the [print](https://web.archive.org/web/20210228003007/https://docs.hyperdbg.org/commands/scripting-language/functions/print) function.

```text
HyperDbg> ? print(@rax);
```

### IOCTL <a id="ioctl"></a>

This commands works over serial by sending the serial packets to the remote computer.

First of all, you should fill the following structure, set the `ScriptBufferSize` and `ScriptBufferPointer` to buffers you got from the script engine interpreter, and leave the `Result`and set the `IsFormat` to **false**.

After that, you should move the interpreted buffer to the end of the structure \(this structure is a header for the interpreted buffer\).

```text
typedef struct _DEBUGGEE_SCRIPT_PACKET {​  UINT32 ScriptBufferSize;  UINT32 ScriptBufferPointer;  BOOLEAN IsFormat;  UINT32 Result;​  //  // The script buffer is here  //​} DEBUGGEE_SCRIPT_PACKET, *PDEBUGGEE_SCRIPT_PACKET;
```

The next step is sending the above structure to the debuggee when debuggee is paused and waiting for new command on **vmx-root** mode.

You should send the above structure with `DEBUGGER_REMOTE_PACKET_REQUESTED_ACTION_ON_VMX_ROOT_RUN_SCRIPT` as `RequestedAction` and `DEBUGGER_REMOTE_PACKET_TYPE_DEBUGGER_TO_DEBUGGEE_EXECUTE_ON_VMX_ROOT` as `PacketType`.

In return, the debuggee sends the above structure with the following type.

```text
DEBUGGER_REMOTE_PACKET_REQUESTED_ACTION_DEBUGGEE_RESULT_OF_RUNNING_SCRIPT
```

In the returned structure, the `Result` is filled by the kernel.

If the `Result` is `DEBUGEER_OPERATION_WAS_SUCCESSFULL`, then the operation was successful. Otherwise, the returned result is an error.

The following function is responsible for sending script buffers in the debugger.

```text
BOOLEAN KdSendScriptPacketToDebuggee(UINT64 BufferAddress, UINT32 BufferLength, UINT32 Pointer, BOOLEAN IsFormat);
```

### Remarks <a id="remarks"></a>

Other aliases for this command are '**eval**' and '**evaluate**'.

This command is guaranteed to keep debuggee in a halt state \(in Debugger Mode\); thus, nothing will change during its execution.

### Requirements <a id="requirements"></a>

None

### Related <a id="related"></a>

None

