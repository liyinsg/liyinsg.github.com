---
layout: post
title: "Microsoft OS descriptors"
---
### OS support
* Microsoft OS 1.0 Descriptors are supported by:
  - Windows 8.1
  - Windows 8
  - Windows 7
  - Windows Vista, Windows Server 2008
  - Windows XP with Service Pack 1 (SP1), Windows Server 2003

* Microsoft OS 2.0 Descriptors are supported by Windows 8.1 onwards

### String Descriptor Request
* Index: 0xEE, langid: 0
* u"MSFT100?", ? is bMS_VendorCode, which will be used for subsequent OS feature vendor request

### OS Feature descriptor
* Genre (0x1)
  - Used by HID devices to provide detailed configuration data. - Not implemented
* Extended Compact ID (0x4), e.g. "WINUSB", "RNDIS"
* Extended Properties (0x5), e.g. URLs, icons, help pages, GUIDs
  - Class level
  - devnode level

### Debugging
* The OS only query 0xEE once
  - because OS will cache the result at HLKM\SYSTEM\CurrentControlSet\Control\UsbFlags\
  - Refer [USB Device Registry Entries](https://msdn.microsoft.com/en-us/library/windows/hardware/jj649946(v=vs.85).aspx) for details
* Make sure the length of CID descriptor is 0x28 for single interface configuration
