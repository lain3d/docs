---
description: Using command-line features
---

# Running HyperDbg Script

There are two ways to run batch-script like commands in **HyperDbg**.

First, you can save your command in a file and then use [.script](https://docs.hyperdbg.com/commands/meta-commands/.script) command and the second way is passing `--script` argument to the **hyperdbg-cli.exe**.

For example, let we saved the following lines in **`c:\users\sina\desktop\script.txt`.**

```bash
.connect local
.logopen c:\users\sina\desktop\result.txt
load
!epthook2 fffff800`4ed6f010 code {488B5A404881FB484442477402EB0848C7424048444232C3}
unload
.logclose
exit
```

Now, if you run **HyperDbg** then you can **.script** command like this :

```bash
HyperDbg >.script c:\users\sina\desktop\script.txt
```

The second case is when you want to directly run your script from the command-line, then you can run the **hyperdbg-cl.exe** like this :

```bash
Microsoft Windows [Version 10.0.18362.900]
(c) 2019 Microsoft Corporation. All rights reserved.

C:\Users\sina\Desktop\HyperDbg>hyperdbg-cli.exe --script c:\users\sina\desktop\script.txt
```

With these two ways, you can automate your scripts in **HyperDbg**.
