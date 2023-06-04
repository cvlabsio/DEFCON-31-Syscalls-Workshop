## LAB Exercise 6: Call Stack Analysis
In this exercise we will focus on call stack analysis and compare the call stacks of all the droppers. We will compare the techniques of direct and indirect syscalls in the context of EDR evasion. We will look at why direct syscalls can be detected by EDRs (depending on the EDR), how indirect syscalls can help in this case, and the limitations of indirect syscalls. 

The main part of this exercise is about how EDRs can use or **analyse** the callstack of a dropper, or more precisely a function, to check whether the return address appears to be legitimate or not. In this chapter we will analyse the callstack of each dropper (Win32, Native, Direct Syscalls and Indirect Syscalls). You can use **Process Hacker** to analyse the callstack. For the tasks in this chapter, you can use the droppers you created in the previous chapters. If you were not able to create all the droppers from the previous chapters, you will find all the completed pocs in the code section of this chapter.

## Exercise 6 Tasks: 
1. Run a standard application such as cmd.exe and analyse the call stack.
2. Run all your droppers step by step, analyse the call stacks and compare them. Which one do you think has the most legitimate call stack?
4. Compare the call stack of the droppers with the call stack of cmd.exe.  
5. Run your direct syscall dropper poc and analyse the call stack.
6. Based on your call stack analysis, why might indirect syscalls help bypass return address checking EDRs compared to direct syscall droppers?
7. Compare the callstack between the native dropper and the indirect syscall dropper. Could the native dropper also be used to bypass EDRs? 


## Default Application Call Stack
As a first step, we want to compare the call stack of a standard application like cmd.exe with the call stack of the Win32 dropper. So we need to run an instance of cmd.exe and the win32 dropper and take a look at the call stack, more specifically we want to take a look at the stack frames from the main function. As mentioned earlier, we want to use Process Hacker to analyse the call stack. To see how Process Hacker can be used for call stack analysis, check out the detail section below. 
<details>
<p align="center">
<img width="400" alt="image" src="https://github.com/VirtualAlllocEx/DEFCON-31-Syscalls-Workshop/assets/50073731/d104651a-be2e-4e91-b276-e93c9a00919d">
</p>
  
You can double-click cmd.exe or right-click and select Properties.
<p align="center"> 
  <img width="500" alt="image" src="https://github.com/VirtualAlllocEx/DEFCON-31-Syscalls-Workshop/assets/50073731/3c5154c8-988c-42e3-8442-d0d866e56b19">
</p>
  
Then we select a thread, again we can double click or right click and select Inspect.
<p align="center">
<img width="500" alt="image" src="https://github.com/VirtualAlllocEx/DEFCON-31-Syscalls-Workshop/assets/50073731/c554c323-ed19-45fd-afb9-523344a41b1d">
</p>
Next we can see the stack frames of the thread. At the top of the stack we can see the last element, and at the bottom the first element. When we say that the stack "grows down", it's important to understand that we're talking about the direction in memory addresses, not a physical direction. On most systems, including Windows, the stack grows from higher to lower memory addresses. This is often described as "down" because if you think of memory addresses laid out from lowest to highest (as in a memory map), then the stack grows from the bottom of this diagram to the top.To be clear, the stack in Windows grows from higher to lower memory addresses. This can be described as the stack growing "down" in memory. However, the "top" of the stack is the current end where operations are taking place, which is at a lower memory address than the "bottom" of the stack.  
</details>

## Win32 Dropper Call Stack
In this step we want to analyse the call stack from the win32 dropper and compare it with the call stack from cmd.exe in the previous step. Remember that in the win32 dropper the control flow is ``dropper.exe`` -> ``kernel32.dll`` -> ``kernelbase.dll`` -> ``ntdll.dll`` -> ``syscall``, based on that what to expect or how the order of the stack frames should look like?




