---
description: Using command-line features
---

# Running HyperDbg Script

There are two ways to run batch-script like commands in **HyperDbg**.

First, we can save our command(s) in a file and then use the [.script](https://docs.hyperdbg.org/commands/meta-commands/.script) command, and the second way is to pass the `--script` argument to the **hyperdbg-cli.exe**.

{% hint style="success" %}
In HyperDbg's batch scripts '`#`' is used as the [comment character](https://docs.hyperdbg.org/commands/debugging-commands/comment). However, in the script engine, it uses a C-like [commenting style](https://docs.hyperdbg.org/commands/scripting-language/assumptions-and-evaluations#comments).
{% endhint %}

For example, let's assume that we can use [.script](https://docs.hyperdbg.org/commands/meta-commands/.script) command like this:

```bash
HyperDbg> .script c:\users\sina\desktop\script.txt
```

The second case is when we want to run our script from the command-line directly; then you can run the **hyperdbg-cli.exe** like this :

```bash
Microsoft Windows [Version 10.0.18362.900]
(c) 2019 Microsoft Corporation. All rights reserved.

C:\Users\sina\Desktop\HyperDbg>hyperdbg-cli.exe --script c:\users\sina\desktop\script.txt
```

With these two ways, we can automate our scripts in **HyperDbg**.
