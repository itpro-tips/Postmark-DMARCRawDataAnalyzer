# Requires -Version 3

$StartDate = '2019-01-01'
$EndDate = '2019-12-31'
$limit = 100
$token = '<your API TOKEN>' # Get yours on https://postmarkapp.com/support/article/1008-what-are-the-account-and-server-api-tokens
$uri = "https://dmarc.postmarkapp.com/records/my/reports?from_date=$StartDate&to_date=$EndDate&limit=$limit"

$headers = @{
    'Accept' = 'application/json'
    'X-Api-Token' = $token
}

$entries = (Invoke-RestMethod -Uri $uri -Method Get -Headers $headers).entries

foreach($entry in $entries)
{    
    $result = Invoke-RestMethod -Uri "https://dmarc.postmarkapp.com/records/my/reports/$($entry.id)" -Method Get -Headers $headers
    
    $records = $result.records
    foreach($record in $records)
    {
        [array]$traces += $record
    } 
}

$traces | ft
