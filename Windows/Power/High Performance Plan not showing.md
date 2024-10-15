# High Performance Plan not showing

## Description
High Performance power plan not showing showing in control panel or not selectable

## Solution
PowerShell
```
$p = Get-CimInstance -Name root\cimv2\power -Class win32_PowerPlan -Filter "ElementName = 'High Performance'"      
powercfg /setactive ([string]$p.InstanceID).Replace("Microsoft:PowerPlan\{","").Replace("}","")
```
