# backtraced

Catch segfaults and show a backtrace, works for both Windows/Linux


# TODO:

- [ ] clean up the code
- [ ] port core.demangle and make it portable (make it work in -betterC)
- [ ] add support for more targets
- [ ] make it work with other languages (static/shared library)

# How to use in my D program:


- Copy paste this file in your project

```D
import bd = backtraced;
void main()
{
  bd.register();
    
  // small test
  int* a;
  *a = 1;
}
```

It should print:

Windows:
```
-------------------------------------------------------------------+
Received signal 'exception' (3221225477ll)
-------------------------------------------------------------------+
C:\tmp\backtraced\app.d:9 - D main
C:\tmp\backtraced\app.d:9 - _D2rt6dmain212_d_run_main2UAAamPUQgZiZ6runAllMFZ9__lambda2MFZv
C:\tmp\backtraced\app.d:9 - _D2rt6dmain212_d_run_main2UAAamPUQgZiZ7tryExecMFMDFZvZv
C:\tmp\backtraced\app.d:9 - _D2rt6dmain212_d_run_main2UAAamPUQgZiZ6runAllMFZv
C:\tmp\backtraced\app.d:9 - _D2rt6dmain212_d_run_main2UAAamPUQgZiZ7tryExecMFMDFZvZv
C:\tmp\backtraced\app.d:9 - _d_run_main2
C:\tmp\backtraced\app.d:9 - _d_run_main
C:\D\dmd2\windows\bin\..\..\src\druntime\import\core\internal\entrypoint.d:29 - app._d_cmain!().main
D:\a\_work\1\s\src\vctools\crt\vcstartup\src\startup\exe_common.inl:288 - __scrt_common_main_seh
D:\a\_work\1\s\src\vctools\crt\vcstartup\src\startup\exe_common.inl:288 - BaseThreadInitThunk
D:\a\_work\1\s\src\vctools\crt\vcstartup\src\startup\exe_common.inl:288 - RtlUserThreadStart
Segmentation fault
```


Linux:
```
-------------------------------------------------------------------+
Received signal 'SIGSEGV' (11)
-------------------------------------------------------------------+
executable: /tmp/dmd_run24uiXx
backtrace: 12
/mnt/c/tmp/backtraced/./app.d:9 _Dmain+0x13
??:? void rt.dmain2._d_run_main2(char[][], ulong, extern (C) int function(char[][])*).runAll().__lambda2()+0x1f
??:? void rt.dmain2._d_run_main2(char[][], ulong, extern (C) int function(char[][])*).tryExec(scope void delegate())+0x22
??:? void rt.dmain2._d_run_main2(char[][], ulong, extern (C) int function(char[][])*).runAll()+0x8b
??:? void rt.dmain2._d_run_main2(char[][], ulong, extern (C) int function(char[][])*).tryExec(scope void delegate())+0x22
??:? _d_run_main2+0x1fb
??:? _d_run_main+0xb8
/home/ryuukk/dlang/dmd-2.102.0/linux/bin64/../../src/druntime/import/core/internal/entrypoint.d:30 main+0x22
??:0 __libc_start_main+0xf3
??:? _start+0x2e
```
