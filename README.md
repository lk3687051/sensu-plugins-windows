## Sensu-Plugins-Windows

[![Build Status](https://travis-ci.org/sensu-plugins/sensu-plugins-windows.svg?branch=master)](https://travis-ci.org/sensu-plugins/sensu-plugins-windows)
[![Gem Version](https://badge.fury.io/rb/sensu-plugins-windows.svg)](http://badge.fury.io/rb/sensu-plugins-windows)
[![Appveyor status](https://ci.appveyor.com/api/projects/status/j6cg9tmxs6ivscrd/branch/master?svg=true)](https://ci.appveyor.com/project/majormoses/sensu-plugins-windows/branch/master)
[![Community Slack](https://slack.sensu.io/badge.svg)](https://slack.sensu.io/badge)

## Functionality

These files provide basic Checks and Metrics for a Windows system.

## Files

### Powershell

 * bin/powershell/check-windows-cpu-load.ps1
 * bin/powershell/check-windows-disk.ps1
 * bin/powershell/check-windows-disk-writeable.ps1
 * bin/powershell/check-windows-pagefile.ps1
 * bin/powershell/check-windows-process.ps1
 * bin/powershell/check-windows-processor-queue-length.ps1
 * bin/powershell/check-windows-ram.ps1
 * bin/powershell/check-windows-service.ps1
 * bin/powershell/metric-windows-cpu-load.ps1
 * bin/powershell/metric-windows-disk-usage.ps1
 * bin/powershell/metric-windows-network.ps1
 * bin/powershell/metric-windows-processor-queue-length.ps1
 * bin/powershell/metric-windows-ram-usage.ps1
 * bin/powershell/metric-windows-uptime.ps1
 * bin/powershell/check-windows-directory.ps1
 * bin/powershell/check-windows-event-log.ps1
 * bin/powershell/check-windows-log.ps1

### Ruby -NOT TESTED-

 * ~~ bin/check-windows-cpu-load.rb~~
 * ~~ bin/check-windows-disk.rb ~~
 * ~~ bin/check-windows-process.rb ~~
 * ~~ bin/check-windows-processor-queue-length.rb ~~
 * ~~ bin/check-windows-ram.rb ~~
 * ~~ bin/check-windows-service.rb ~~
 * ~~ bin/metric-windows-cpu-load.rb ~~
 * ~~ bin/metric-windows-disk-usage.rb ~~
 * ~~ bin/metric-windows-network.rb ~~
 * ~~ bin/metric-windows-processor-queue-length.rb ~~
 * ~~ bin/metric-windows-ram-usage.rb ~~
 * ~~ bin/metric-windows-uptime.rb ~~
 * ~~ bin/powershell_helper.rb ~~


## Usage

##### Example 1:

Check Definition

```json
{
  "type": "CheckConfig",
  "api_version": "core/v2",
  "metadata": {
    "namespace": "default",
    "name": "win-cpu-check"
  },
  "spec": {
    "command": "powershell.exe -ExecutionPolicy ByPass -C check-windows-cpu-load.ps1 90 95",
    "subscriptions": [
      "windows"
    ],
    "handlers": [
      "slack",
      "email"
    ],
    "runtime_assets": [
      "sensu-plugins-windows"
    ],
    "interval": 60,
    "publish": true
  }
}
```

Asset Definition

```json
{
  "type": "Asset",
  "api_version": "core/v2",
  "metadata": {
    "name": "sensu-plugins-windows-checks",
    "namespace": "default",
    "labels": {},
    "annotations": {}
  },
  "spec": {
    "url": "[RESOURCE_URL]",
    "sha512": "[EXAMPLE SHA512sum 7478720b02451aedc2]",
    "filters": [
      "entity.system.os == 'windows'",
      "entity.system.arch == 'amd64'"
    ]
  }
}
```

## Dependencies
 * Powershell checks require Powershell version 3.0 or higher.

## Troubleshooting
* Failures to pull counter data with messages like below, might be due to corrupt performance counters. See [Here](https://support.microsoft.com/en-us/help/2554336/how-to-manually-rebuild-performance-counters-for-windows-server-2008-6) for more information.  Short answer on fix is `lodctr /R` in an Admin elevated command prompt

## Installation

TO DO
