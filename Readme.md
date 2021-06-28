```Ruby
$FinalChange = $null ;   $modification =$null
$names         = Import-Csv -Path C:\temp\names.csv
$FinalChange   = @()
class newTable{
    [string]$name
    [string]$Language
    [string]$dob
}


foreach($name in $names){
    $modification = [newTable]::new()
    $modification.name     = $name.Name
    $modification.Language = $name.Language
    $modification.dob      = (get-date -Format 'yyyy').ToString()
    $FinalChange += $modification
}
$FinalChange | Export-Csv C:\temp\names.csv -NoTypeInformation
```
