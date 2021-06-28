Sample of a CSV before changes:

![image](https://user-images.githubusercontent.com/44326428/123570561-15713280-d78e-11eb-8053-4ab5d6cac7b8.png) </br>


The script below will change:
* The whole content in cell, from column **'dob'**
* It will break the content in cell, from column **'convention'** , and convert it back to its current convention like so:
    *   USA
    *   2 digit's current Month 
    *   The rest of the string


```Ruby
$FinalChange   = $null ;   $modification =$null
$names         = Import-Csv -Path C:\temp\names.csv
$FinalChange   = @()
$month         = (get-date -Format 'MM').ToString()

class newTable{
    [string]$name
    [string]$Language
    [string]$dob
    [string]$convention
}

foreach($name in $names){
    $modification            = [newTable]::new()
    $modification.name       = $name.Name
    $modification.Language   = $name.Language
    $modification.dob        = '1981'

    $namingStartW = $name.conventionMonthName.Substring(0,3)
    $namingEndW   = $name.conventionMonthName.Substring(5,5)
    $modification.convention = $namingStartW + $month + $namingEndW

    $FinalChange += $modification
}
$FinalChange | Export-Csv C:\temp\names.csv -NoTypeInformation
```

Once done, the new object will take over the old csv file with the new edits.</br>
final output example: </br>
![image](https://user-images.githubusercontent.com/44326428/123571903-d2648e80-d790-11eb-9ba1-6013a80b6f64.png)




