Sample of a CSV before changes:</br>
![image](https://user-images.githubusercontent.com/44326428/123723640-74977b80-d850-11eb-9288-6bacc3319846.png)</br>


The script below will change:
* The whole content in cell, from column **'dob'**
* It will break the content in cell, from column **'convention'** , and convert it back to its current convention like so:
    *   USA
    *   2 digit's current Month 
    *   The rest of the string


```Ruby
Clear-Host
$FinalChange   = $null ;   $modification =$null
$names         = Import-Csv -Path C:\temp\names.csv
$FinalChange   = @()
$month         = (get-date -Format 'MM').ToString()

class newTable{
    [string]$name
    [string]$Language
    [string]$dob
    [string]$NickName
    [string]$convention
}

foreach($name in $names){
    $modification            = [newTable]::new()
    $modification.name       = $name.Name
    $modification.Language   = $name.Language
    $modification.dob        = '1981'
    $modification.NickName   = $name.NickName

    $namingStartW = $name.convention.Substring(0,3)
    $namingEndW   = $name.convention.Substring(5,5)
    $modification.convention = $namingStartW + $month + $namingEndW

    $FinalChange += $modification
}

$FinalChange | FT -AutoSize
Write-Host "The changes will be made like so:"
Write-Host "Press any key to continue..."
PAUSE
#Start-Sleep -Seconds 3

$FinalChange | Export-Csv C:\temp\names.csv -NoTypeInformation
```

Once done, the new object will take over the old csv file with the new edits.</br>
final output example: </br>
![image](https://user-images.githubusercontent.com/44326428/123725220-5c752b80-d853-11eb-9871-6389f76b9514.png)
