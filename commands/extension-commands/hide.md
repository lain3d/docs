---
description: Description of '!hide' command in HyperDbg.
---

# !hide \(enable transparent-mode\)

### Command

> !hide

### Syntax

> !hide

### Description

Enables the transparent-mode of **HyperDbg** for anti-debugging and anti-hypervisor methods.

### Parameters

None

### Examples

```text
HyperDbg >!hide
```

### IOCTL

You should send the `IOCTL_DEBUGGER_HIDE_AND_UNHIDE_TO_TRANSPARENT_THE_DEBUGGER` IOCTL to enable or disable transparent-mode.

The following structure shows whether enable or disable it.

`IsHide = TRUE` : Enable transparent-mode.

`IsHide = FALSE`: Disable transparent-mode.

```c
typedef struct _DEBUGGER_HIDE_AND_TRANSPARENT_DEBUGGER_MODE {

  BOOLEAN IsHide;
  UINT64 KernelStatus; /* DEBUGEER_OPERATION_WAS_SUCCESSFULL ,
                          DEBUGEER_ERROR_UNABLE_TO_HIDE_OR_UNHIDE_DEBUGGER
                          */

} DEBUGGER_HIDE_AND_TRANSPARENT_DEBUGGER_MODE,
    *PDEBUGGER_HIDE_AND_TRANSPARENT_DEBUGGER_MODE;
```

If the results were successful then kernel sends `DEBUGEER_OPERATION_WAS_SUCCESSFULL` to user-mode and if it was unsuccessful then `DEBUGEER_ERROR_UNABLE_TO_HIDE_OR_UNHIDE_DEBUGGER` which is an indicator of error.

### **Remarks**

This command will not guarantee to provide 100% transparency.

**HyperDbg** will not protect you from anti-VMware, anti-VirtualBox, etc. methods, instead, it tries to hide itself from anti-debugging and anti-hypervisor methods thus you need to run this command in a physical-machine \(not in a nested-virtualization environments\).

### Requirements

None

### Related

[!unhide \(disable transparent-mode\)](https://docs.hyperdbg.com/commands/extension-commands/unhide)
