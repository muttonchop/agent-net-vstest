[![Build status](https://ci.appveyor.com/api/projects/status/0bgatrnrtl1r1prm/branch/master?svg=true)](https://ci.appveyor.com/project/nvborisenko/agent-net-vstest/branch/master)

# Installation
[![NuGet version](https://badge.fury.io/nu/ReportPortal.VSTest.TestLogger.svg)](https://badge.fury.io/nu/ReportPortal.VSTest.TestLogger)

Install **ReportPortal.VSTest.TestLogger** NuGet package into your project with tests.

# Configuration
Add new **ReportPortal.config.json** file into your project with *Copy if newer* value for *Copy to Output Directory* property.

Example of config file:
```json
{
  "$schema": "https://raw.githubusercontent.com/reportportal/agent-net-vstest/master/ReportPortal.VSTest.TestLogger/ReportPortal.config.schema",
  "enabled": true,
  "server": {
    "url": "https://rp.epam.com/api/v1/",
    "project": "default_project",
    "authentication": {
      "uuid": "7853c7a9-7f27-43ea-835a-cab01355fd17"
    }
  },
  "launch": {
    "name": "VS Test Demo Launch",
    "description": "this is description",
    "debugMode": true,
    "tags": [ "t1", "t2" ]
  }
}
```
# Results publishing
To publish test results in real-time to the ReportPortal specify `Logger` argument.

## vstest.console.exe
```cmd
vstest.console.exe MyTests.dll /TestAdapterPath:. /Logger:ReportPortal
```
## dotnet vstest
```cmd
dotnet vstest MyTests.dll --logger:ReportPortal
```

> In case if you see `Could not find a test logger with AssemblyQualifiedName, URI or FriendlyName 'ReportPortal'.` error message after executing tests, and your target framework is **netcoreapp**, it's recommended to make `dotnet publish` before executing tests. It's needed to copy TestLogger with dependencies to output folder, so vstest is able to discover TestLogger.

# Parameters overriding
```cmd
--logger:ReportPortal;Launch.Name="My new launch name"
```

## Supported parameters
- `Launch.Name`
- `Launch.Description`
- `Launch.Tags` - comma-separated list
- `Launch.IsDebugMode` - true/false

- `Server.Project`
- `Server.Authentication.Uuid`

