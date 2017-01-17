# Functions

- [CloseHandle](#CloseHandle)
- [CreateToolhelp32Snapshot](#CreateToolhelp32Snapshot)
- [GetLastError](#GetLastError)
- [Module32First](#Module32First)
- [Module32Next](#Module32Next)
- [OpenProcess](#OpenProcess)
- [ReadBytes](#ReadBytes)
- [ReadCString](#ReadCString)
- [ReadInt16](#ReadInt16)
- [ReadInt32](#ReadInt32)
- [ReadInt64](#ReadInt64)
- [ReadInt8](#ReadInt8)
- [SetLastError](#SetLastError)
- [Sleep](#Sleep)

## CloseHandle

```lua
local kernel32 = require("winapi_kernel32")

local hHandle = -- previously acquired HANDLE

-- BOOL
local result = kernel32.CloseHandle(hHandle)
```

## CreateToolhelp32Snapshot

```lua
local kernel32 = require("winapi_kernel32")

local TH32CS_SNAPMODULE = 0x8

-- HANDLE
local hSnapshot = kernel32.CreateToolhelp32Snapshot(
    TH32CS_SNAPMODULE, -- DWORD dwFlags
    1234 -- DWORD th32ProcessID
)
```

## GetLastError

```lua
local kernel32 = require("winapi_kernel32")

-- DWORD dwErrCode
local error = kernel32.GetLastError()
```

## Module32First

```lua
local kernel32 = require("winapi_kernel32")

local hSnapshot = -- previously acquired HANDLE

local result, me32 = kernel32.Module32First(
    hSnapshot -- HANDLE hSnapshot
)

if (result) then
    print("module name: ", me32.szModule)
end
```

## Module32Next

```lua
local kernel32 = require("winapi_kernel32")

local hSnapshot = -- previously acquired HANDLE

local result, me32 = kernel32.Module32Next(
    hSnapshot -- HANDLE hSnapshot
)
if (result) then
    print("module name: ", me32.szModule)
end
```

## OpenProcess

```lua
local kernel32 = require("winapi_kernel32")

local PROCESS_ALL_ACCESS = 0x1F0FFF

-- HANDLE
local hProcess = kernel32.OpenProcess(
    PROCESS_ALL_ACCESS, -- DWORD dwDesiredAccess
    false, -- BOOL bInheritHandle
    1234 -- DWORD dwProcessId
)
```

## ReadBytes

This method is intended to supply a work around
ReadProcessMemory.

**Summary**: Reads n bytes from the process handle and returns
the data (exactly n bytes) as a Lua string

```lua
local kernel32 = require("winapi_kernel32")

local hProcess = -- previously acquired HANDLE

-- BOOL, string, SIZE_T
local result, data, numberOfBytesRead = kernel32.ReadBytes(
    hProcess, -- HANDLE hProcess
    0x40000000, -- number lpBaseAddress
    10 -- DWORD numberOfBytesToRead
)

if (result) then
    assert(#data == 10)
    
    local byte

    for i = 1, #data do
        -- data is a regular Lua string, so
        -- you can access i-th byte
        -- this way
        local byte = data:sub(i, i):byte()
    end
end
```

## ReadCString

This method is intended to supply a work around
ReadProcessMemory.

**Summary**: Reads n bytes from the process handle and returns
the data (up to the NULL-terminated character or n)
as a Lua string

```lua
local kernel32 = require("winapi_kernel32")

local hProcess = -- previously acquired HANDLE

-- BOOL, string, SIZE_T
local result, data, numberOfBytesRead = kernel32.ReadCString(
    hProcess, -- HANDLE hProcess
    0x40000000, -- number lpBaseAddress
    10 -- DWORD numberOfBytesToRead
)

if (result) then
    print(data)
end
```

## ReadInt16

This method is intended to supply a work around
ReadProcessMemory.

**Summary**: Reads 16 bits from the process

```lua
local kernel32 = require("winapi_kernel32")

local hProcess = -- previously acquired HANDLE

-- BOOL, INT16, SIZE_T
local result, data, numberOfBytesRead = kernel32.ReadInt16(
    hProcess, -- HANDLE hProcess
    0x40000000, -- number lpBaseAddress
)

if (result) then
    print(data)
end
```

## ReadInt32

This method is intended to supply a work around
ReadProcessMemory.

**Summary**: Reads 32 bits from the process

```lua
local kernel32 = require("winapi_kernel32")

local hProcess = -- previously acquired HANDLE

-- BOOL, INT32, SIZE_T
local result, data, numberOfBytesRead = kernel32.ReadInt32(
    hProcess, -- HANDLE hProcess
    0x40000000, -- number lpBaseAddress
)

if (result) then
    print(data)
end
```

## ReadInt64

This method is intended to supply a work around
ReadProcessMemory.

**Summary**: Reads 64 bits from the process

```lua
local kernel64 = require("winapi_kernel64")

local hProcess = -- previously acquired HANDLE

-- BOOL, INT64, SIZE_T
local result, data, numberOfBytesRead = kernel64.ReadInt64(
    hProcess, -- HANDLE hProcess
    0x40000000, -- number lpBaseAddress
)

if (result) then
    print(data)
end
```

## ReadInt8

This method is intended to supply a work around
ReadProcessMemory.

**Summary**: Reads 8 bits from the process

```lua
local kernel32 = require("winapi_kernel32")

local hProcess = -- previously acquired HANDLE

-- BOOL, INT8, SIZE_T
local result, data, numberOfBytesRead = kernel32.ReadInt8(
    hProcess, -- HANDLE hProcess
    0x40000000, -- number lpBaseAddress
)

if (result) then
    print(data)
end
```

## SetLastError

```lua
local kernel32 = require("winapi_kernel32")

kernel32.SetLastError(
    1234 -- DWORD dwErrCode
)
```

## Sleep

```lua
local kernel32 = require("winapi_kernel32")

kernel32.Sleep(
    1000 -- DWORD dwMilliseconds
)
```