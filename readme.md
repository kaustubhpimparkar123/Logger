# Logger
* [General Info](#motivation)
* [Reference](#reference-contents)
## A simple thread-safe single-header C++ 17 logger.
### Motivation
To create a simple, thread safe logger in C++
### Simple Example
Console logging (the simplest use case)
```cpp
#include "src/logger.h"

int main()
{
	const char* name = "User";
	LOG_INFO("Hello %s", name);

	// LOG_CRITICAL("OH NO!", name);
	
	return 0;
}
```
Output:
> 09/15/21 19:58:45       [Info]  Hello User on line 13 in main.cpp 


###  Quick Start
Logger doesn't need to be instantiated, just include the header and use it like this
```cpp
	LOG_INFO("Information %d", number);
```
Newline character at the end of the message will be done added automatically.


## Reference Contents
* [Log Priorities](#log-priorities)
* [Logging](#logging)
* [File Output](#file-output)
* [Timestamps](#timestamps)

## Reference

### Log Priorities
The default log priority is `Logger::InfoPriority`. You can set priority by calling
```cpp
	Logger::SetPriority(Yellog::DebugPriority);	// e.g. Yellog::DebugPriority
```

Possible values:
```cpp
	Logger::TracePriority
	Logger::DebugPriority
	Logger::InfoPriority
	Logger::WarnPriority
	Logger::ErrorPriority
	Logger::CriticalPriority
```
  
You can get priority by calling
```cpp
	Logger::GetPriority();	// will return Yellog::InfoPriority if Yellog::SetPriority hasn't been called before
```


### Logging
To log:
```cpp
	LOG_TRACE(const char* Message, Args ...args)		// log a message with trace priority
	LOG_DEBUG(const char* Message, Args ...args)		// log a message with debug priority
	LOG_INFO(const char* Message, Args ...args) 		// log a message with info priority
	LOG_WARN(const char* Message, Args ...args)		// log a message with warn priority
	LOG_ERROR(const char* Message, Args ...args)		// log a message with error priority
	LOG_CRITICAL(const char* Message, Args ...args)		// log a message with critical priority
```

As args you can provide primitives and C-strings. Formatting follows [printf format](https://www.cplusplus.com/reference/cstdio/printf/).


### File Output
To enable file output, call
```cpp
	Logger::EnableFileOutput("mylogpath/mylog.txt");
```
before using the logger.  
  
Optionally, you can provide no path
```cpp
	Logger::EnableFileOutput();
```
then, the logs will be saved in '/log.txt'.  
  
To get the current filepath for file logging, call
```cpp
	Logger::GetFilepath();
```
if file output was not enabled, the filepath will contain NULL, otherwise a const char* value will be returned.  
  
To check if file output was enabled and file was successfully opened, call
```cpp
	Logger::IsFileOutputEnabled();	// returns true if success, false if failure
```


### Timestamps
Format follows ctime [strftime format specification](https://www.cplusplus.com/reference/ctime/strftime/).  
Default format is "%T  %d-%m-%Y" (e.g. 13:20:25  14-02-2021).  
4 spaces are added automatically to the end of timestamp each time the message is logged.  

  
