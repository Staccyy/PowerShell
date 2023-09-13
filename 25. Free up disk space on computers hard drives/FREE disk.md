#1 Removing recycle bin files 
#set the path to the recycle bin on the C:
$path = 'C:$recycle.bin'

#get all items (files and directories) within the recycle bin path, including hidden ones
$items = Get-ChildItem $path -Force -Recurse -ErrorAction SilentlyContinue

#remove the items, excluding any files with the .ini extension
$items | Remove-Item -Recurse -Exclude *.ini -ErrorAction SilentlyContinue

#2 remove temp files from various locations

#specify the path where temporary files are stored in the windows Temp folder
Get-ChildItem $path1 -Force -Recurse -ErrorAction SilentlyContinue | Remove-Item -Recurse -force -ErrorAction SilentlyContinue

#specify the path where the temporary files are stored in the windows Prefetch folder
$path2 = 'C:\Windows\Prefetch'

#remove all items (files and directories) from the windows prefetch folder
Get-ChildItem $path2 -Force -Recurse -ErrorAction SilentlyContinue | Remove-Item -Recurse -Force -ErrorAction SilentlyContinue

#Specify the path where temporary files are stored in the user's Appdata\local\temp folder
$path3 = 'C:users\*\appdata\local\temp'

#remove all items (files and directories) from the specified users temp folder
Get-ChildItem $path3 -Force -Recurse -ErrorAction SilentlyContinue | Remove-Item -Recurse -Force -ErrorAction SilentlyContinue

#display a success message 
Write-Host "removed all the temp files successfully" -ForegroundColor Green

#3 Using disk cleanup tools

#display a message indicating the usage of the disk cleanup tool
Write-host "using disk cleanup tool" -ForegroundColor Yellow

#run the disk cleanup tool with the specified sagerun parameter
cleanmgr /sagerun:1 | Out-Null

#emit a beep sound using ASCII code 7
Write-Host "$([char]7)"

#Pause the script for 5 seconds
Sleep 5

#Display a success message indicating that disk cleanup was successfully done 
Write-Host "disk cleanup Successfully done" -ForegroundColor Green

#Pause the script for 10 seconds
Sleep 10 