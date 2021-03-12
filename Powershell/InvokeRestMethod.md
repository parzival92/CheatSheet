## Invoke-RestMethod

The Invoke-RestMethod cmdlet sends HTTP and HTTPS requests to Representational State Transfer (REST) web services that return richly structured data.

The ConvertFrom-Json cmdlet converts a JavaScript Object Notation (JSON) formatted string to a custom PSCustomObject object that has a property for each field in the JSON string.

```
$Yourjsonbody = Get-Content -Raw -Path $jsonfile | ConvertFrom-Json
$Thumbprint="If authentication mode is pfx file it will generate thumbprint"
Try {
$Result = Invoke-RestMethod -Uri $url -Method Put -Body $Yourjsonbody -ContentType "application/json" -CertificateThumbprint $Thumbprint -Headers @{ }
}
Catch {
    if($_.ErrorDetails.Message) {
        Write-Host $_.ErrorDetails.Message
    } else {
        Write-Host $_
    }
```

```
$user = $ClusterUser
$pass = $ClusterPassword

$pair = "$($user):$($pass)"

$encodedCreds = [System.Convert]::ToBase64String([System.Text.Encoding]::ASCII.GetBytes($pair))

$headers = New-Object "System.Collections.Generic.Dictionary[[String],[String]]"
$headers.Add("X-Requested-By", "*****")
$headers.Add("Content-Type", "application/x-www-form-urlencoded")
$headers.Add("Authorization", "Basic $encodedCreds")

$body = "{Any json body}"

try
{
$response = Invoke-RestMethod 'url' -Method 'POST' -Headers $headers -Body $body
if ($response.StatusCode -lt 201){
   Write-Host "Request Sucessfull"
}
}
catch
{
    $StatusCode = $_.Exception.Response.StatusCode.value__
}
Write-Host $StatusCode
```
