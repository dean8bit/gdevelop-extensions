A repository for my GDevelop extensions

# CPU Extension
A CPU Emulator with various instruction sets, extensible instrution sets. must be ineracted with in javascript code blocks. use with the UILayer to get a html multiline text input

1. Create an 'at the beginning of the scene' and add the InitCPU action
2. this binds the cpu to the runtimeGame object
3. Add a javascript block and add
```
const runtimeGame = runtimeScene.getGame();

//create a cpu with 32 memory, basic instructionset, and a fib sequence code
const cpuInstance = runtimeGame.CPUDefinition.CreateCPU(32, runtimeGame.CPUDefinition.InstructionSets.BASIC.Instructions,
[
    "--comment Fibonacci",
    "SET #0 24",
    "SET #2 5",
    "SET #4 1 --comment",
    "--comment",
    "LBL 0",
    "SET >2 #3",
    "ADD >2 #4",
    "SET #3 #4",
    "SET #4 >2",
    "ADD #2 1",
    "SUB #0 1",
    "JLZ #0 1",
    "JMP 0",
    "LBL 1",
]);

// step the cpu and 
const output = cpuInstance.step()
cpuInstance.step()
cpuInstance.step()
const memoryValue = cpuInstance.memory.getAt(1)
cpuInstance.memory.setAt(1, 12345)
// call cpuInstance.parse('code here') to update code
// refer to code in extension for more information
...
```

# JavaScript Worker Parser
A Isolated Worker for executing user entered javascript in a eval() function. must be ineracted with in javascript code blocks. use with the UILayer to get a html multiline text input. 

1. Create an 'at the beginning of the scene' condition and add the InitialiseWorker action
2. this binds the worker object to the runtimeGame object
3. add a javascript block

```
const runtimeGame = runtimeScene.getGame();

// a message from the worker object
runtimeGame.worker.onmessage = (event) => {
        if (event.data.toString().includes("TRYERROR:")) console.log(event.data); //handle error
        else console.log(event.data); //do something else with it
    };

// a message to the worker object containing code
runtimeGame.worker.postMessage("const header = [1,2,3,4];console.log(header);") 
```
2. Worker returns 'TRYERROR:...' if the worker comes across a try catch error.


# UI Layer
Creates a div in the html body floating above the game window, for inserting html ui elements, this allows for more advanced ui elements offered by html

1. Create an 'at the beginning of the scene' condition and add the InitialiseUILayer action
2. add a javascript block
```
const ui = document.getElementById('ui');
// add elements to ui, alter style, etc
```
