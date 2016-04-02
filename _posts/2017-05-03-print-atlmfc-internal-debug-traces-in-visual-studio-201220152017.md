---
layout: post
title: "Print ATL/MFC internal traces in Visual Studio 2012/2015/2017"
---
### Prior Visual Studio 2012, Microsoft provided a tool [ATL/MFC Trace Tool](https://msdn.microsoft.com/en-us/library/ms241448(v=vs.80).aspx) to output trace messages in Visual Studio's output debugging window.
![ATLMFCTraceTool](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Components.PostAttachments/00/09/90/45/05/ATL%20MFC%20Trace%20Tool%20and%20the%20Tracing%20Mehanism.png)
To use the ATL/MFC Trace Tool,
* Open an MFC or an ATL project.
* On the Debug menu, click Start Debugging.
* On the Tools menu, click ATL/MFC Trace Tool.

### However this tool is removed from VS2012, and missing `atldebugapi.h` if build from source.
I figured out that there is a major change in ATL/MFC after reading the source code.
Add the following code in your code, e.g. CWinApp::InitInstance(), will enable full traces:
```c++
ATL::CTrace::SetCategories(ATL::CTrace::EnableAllCategories);
ATL::CTrace::SetLevel(ATL::CTrace::DisableTracing - 1);
```

