# tsc-error-library
The TSC Error Library is a common error handling approach that can be utilized in LabVIEW-based applications.

Software is going to have errors. `Local Error Handling` means handling the error at the place in code where it may occur. `Global Error Handling` is for those errors that are unknown and may pop up intermittently or at any point because of some issue.

These functions are meant to handle `Global Errors` that don't have a local solution or are not known at the current release.

It's time to make better code and to...:

<img src="./assets/images/(error) pexels-brett-jordan-6700369.jpg" alt = "Own Your Error"  width = 560 height = 420/>

## Initialize Error Handling
<img src="./assets/images/(error) Init Error Loop.PNG" alt = "Initialize Error Handling" />

## Main Error Loop
<img src="./assets/images/(error) Error Loop.PNG" alt = "Main Error Loop" />

## Stop Error Loop
<img src="./assets/images/(error) Stop Error Loop.PNG" alt = "Main Error Loop" />

## Example Usage
<img src="./assets/images/(error) Example.PNG" alt = "Error Example" /> 
Above is a simplified example of using the TSC Error Handling library in an application.
Init Error Loop - is using all three optional inputs

`UI Update` Queue - if an error occurs, the Error-Prompt message is going to send out a message to a queue and would contain:Message = "ERROR-Prompt"

`Data` = a string containing the error message

Giving a reference to a queue is so that the application can handle prompting the user in the desired format/method; in this example the message would go to the UI Update Loop which could respond to the `ERROR-Prompt` message in a developer-defined way. 

Often handling includes letting the user know that the error has occurred and giving an opportunity to safely shut down or continue with program execution.

`Error Log` - a path to the output error log file (all global errors are logged automatically); if this is undefined, it will be created in "error.txt" at the application directory

`Application Errors` - a path to a customized file of error codes for the application

**Error Loop** needs to be included in the main application to handle global errors; the function `Handle Errors.vi` will send all unhandled errors to this loop. It will automatically log the error to a defined location and will send out the message described above to the queue reference if it exists.

**Stop Error Loop** should be called as part of the main shut down procedure so that Error Loop.vi will be stopped. It MUST NOT be dependent on the output of Error Loop.vi.

<img src="./assets/images/(error) handle errors.PNG" alt = "Handle Errors.vi" />

**Handle Errors** SHOULD be placed at the end of any behavior that needs to send errors to the global Error Loop for handling. This function only runs when an error is input to its error in terminal and will call the messages in the Error Loop. There is an optional input for **Prompt?** which is default to true which will send the message described above or ignore the message.

