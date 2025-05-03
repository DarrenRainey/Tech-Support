# Winlogbeat - Bulk EVTX Import

## Description
Importing a large amount of Windows Event logs (.evtx) files can take a long time if done sequentially or manually.

## Solution
Using the code below and Powershell 7 you can export logs in batches of [x] at a time (Adjust filepath and throttlelimit as appropriate.
Example below runs through all files located in F:\Logs with a limit of 50 files at time (This will spawn 50 copies of winlogbeat - 1 per file be sure to adjust for your system load)

```
[System.Collections.ArrayList]$remaingFiles = (Get-ChildItem -File 'F:\Logs\').FullName
$remaingFiles | ForEach-Object -Parallel { 
$file = $_;
$reg = (Get-Random).toString() +".yml" # Create temp folder to avoid conflicts with multiple copies running
.\winlogbeat.exe -c .\final.yml -E EVTX_FILE="$file" -E REG_FILE="$reg" -E DATA_PATH="$reg-data"
echo "Finsihed $file"
rm $reg-data -Recurse
} -ThrottleLimit 50
```
