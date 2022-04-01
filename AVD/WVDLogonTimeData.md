#WVDLogonTimeData

Here is KQL query to see the user AVD logon time data:

```
WVDCheckpoints 
| where Name == "LogonDelay"
| extend
    LogonType=Parameters.LogonType,
    AuthenticateUser=Parameters.AuthenticateUser,
    GPClient=Parameters.WinLogon_Logon_GPClient,
    Profiles=Parameters.WinLogon_Logon_Profiles,
    Sens=Parameters.WinLogon_Logon_Sens,
    SessionEnv=Parameters.WinLogon_Logon_SessionEnv,
    TermSrv=Parameters.WinLogon_Logon_TermSrv,
    frxsvc=Parameters.WinLogon_Logon_frxsvc,
    StartShell=Parameters.WinLogon_StartShell,
    WinLogon_Logon=Parameters.WinLogon_Logon,
    WinLogon_Total=Parameters.WinLogon_Total
| where LogonType == "DirectSession"
| project-away
    Parameters,
    _ResourceId,
    _SubscriptionId,
    SourceSystem,
    TenantId,
    Type,
    Source,
    Name,
    ActivityType,
    LogonType,
    CorrelationId
| project-reorder TimeGenerated, UserName
```