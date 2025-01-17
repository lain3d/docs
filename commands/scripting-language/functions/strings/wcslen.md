---
description: Description of 'wcslen' function in HyperDbg Scripts
---

# wcslen

### Function

> wcslen

### Syntax

> wcslen( Expression );

### Parameters

**\[Expression (Address)]**

A [MASM-like expression](https://docs.hyperdbg.org/commands/scripting-language/assumptions-and-evaluations) to evaluate which is the address of the target location to compute the string length.

### Description

Counts the length of the wide-character string from an address.

### Return value

The return value is the length of the strings which is located at the target address. If there is an error or if the address is invalid then, it returns `0`.

### Examples

`StringLen = wcslen(@rcx + 10);`

Adds 0x10 to the **rcx** register and counts the length of the wide-character string, which is determined by the terminating double null-character and saves the result into `StringLen` variable.

`StringLen = wcslen(dq(@rcx));`

Counts wide-character string length as an 8-byte hex address, pointed by **rcx** register and saves the result into `StringLen` variable.

`StringLen = wcslen(0xffff83811f265040);`

Counts wide-character string length located at `0xffff83811f265040` address and saves the result into `StringLen` variable.

### Remarks

None

### Related

[strlen](https://docs.hyperdbg.org/commands/scripting-language/functions/strings/strlen)
