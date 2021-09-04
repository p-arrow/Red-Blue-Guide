*Hint: sysmon provides more details than WinEventLogs (!)*

## How To Modify

1) gpedit.msc
2) Win Settings -> Sec Settings -> Local Policies -> Audit Policy
3) Adjust Settings
4) gpupdate (!)

## Change Maximum Log Size

1) gpedit.msc
2) Win Settings -> Sec Settings - Right Click -> Properties

## Severity Level
- Critical (most severe)
- Error
- Warning
- Informational
- Verbose (least severe)
- Audit Success/Failure

## Best Practice

![grafik](https://user-images.githubusercontent.com/84674087/132098709-31cc1a6c-ebfd-47d3-a967-9a99f95c6d35.png)


## Event IDs (typical)

- 4624: logon event
- 4625: failed logon event
- 4688: new process created
- 4740: account lockout
- 4648: attempt to logon with explicit credentials
- 5025: windows firewall service has stopped
- 1102: log was cleared
- 4767: user account was unlocked
- 4657: registry value was changed
- 4616: system time was changed
- 4719: system audit policy was changed
- 4825: denied access via RDP
