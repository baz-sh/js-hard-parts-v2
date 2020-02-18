# JavaScript Principles

## Thread of Execution

When JS runs it goes through code line-by-line and 'executes' each line. This is known as the **thread of execution**.

If it comes across data or functions, it stores this in memory for later use.

When we define a function we create an _identifier_ which we store in memory. We store the code in the function in memory.

## Functions

Code we save (`define`) and code we can use (call/invoke/execute/run) later with the function name & ()

'Execution context' is created and used to run the function. This has two parts; thread of execution and memory. This memory is allocated within the function and used only for the purposes of that function. e.g. any variables created etc are placed in the "memory" within the functions execution context.

![context](/img/01-context.png)

## Call Stack

The call stack is a stack data model that works from the global context, when a function is run, that's placed to the top of the stack and begins to run. If that function invokes another function then that function is added to the top of the stack. Once execution finishes, it pops the current context off the stack and returns to the previous call site. When no call sites remain, the stack is the global context.

![call-stack](/img/01-callstack.png)

We keep track of the functions we are running and where the thread of exection is using the callstack.
