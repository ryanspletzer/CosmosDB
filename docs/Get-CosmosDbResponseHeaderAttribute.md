---
external help file: CosmosDB-help.xml
Module Name: CosmosDB
online version:
schema: 2.0.0
---

# Get-CosmosDbContinuationToken

## SYNOPSIS

Return an attribute from a response header object.

## SYNTAX

```powershell
Get-CosmosDbResponseHeaderAttribute [-HeaderName] <String> [-ResponseHeader] <Object> [<CommonParameters>]
```

## DESCRIPTION

This function takes a response header object that is generated by the ResponseHeader
reference parameter in the Get-CosmosDbCollection or Get-CosmosDbDocument functions
and returns an attribute matching the HeaderName.

If the header is missing or empty in the ResponseHeader then an empty string will
be returned.

## EXAMPLES

### Example 1

### Example 5

```powershell
PS C:\> $ResponseHeader = $null
PS C:\> $indexStringRange = New-CosmosDbCollectionIncludedPathIndex -Kind Range -DataType String -Precision -1
PS C:\> $indexNumberRange = New-CosmosDbCollectionIncludedPathIndex -Kind Range -DataType Number -Precision -1
PS C:\> $indexIncludedPath = New-CosmosDbCollectionIncludedPath -Path '/*' -Index $indexStringRange, $indexNumberRange
PS C:\> $newIndexingPolicy = New-CosmosDbCollectionIndexingPolicy -Automatic $true -IndexingMode Consistent -IncludedPath $indexIncludedPath
PS C:\> Set-CosmosDbCollection -Context $cosmosDbContext -Id 'MyExistingCollection' -IndexingPolicy $newIndexingPolicy
PS C:\> $collections = Get-CosmosDbCollection -Context $cosmosDbContext -Id 'MyExistingCollection' -ResponseHeader ([ref] $ResponseHeader)
PS C:\> $indexUpdateProgress = Get-CosmosDbResponseHeaderAttribute -ResponseHeader $ResponseHeader -HeaderName 'x-ms-documentdb-collection-index-transformation-progress'
```

Update a collection with a new indexing policy and retrieve the index transformation
progress.

## PARAMETERS

### -HeaderName

The name of the Header to return from the Response Headers.

```yaml
Type: String
Parameter Sets: (All)
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### -ResponseHeader

The Response Header object generated by Get-CosmosDbCollection or Get-CosmosDbDocument
functions.

```yaml
Type: Object
Parameter Sets: (All)
Aliases:

Required: True
Position: 0
Default value: None
Accept pipeline input: False
Accept wildcard characters: False
```

### CommonParameters

This cmdlet supports the common parameters: -Debug, -ErrorAction, -ErrorVariable,
-InformationAction, -InformationVariable, -OutVariable, -OutBuffer, -PipelineVariable,
-Verbose, -WarningAction, and -WarningVariable. For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216).

## INPUTS

### None

## OUTPUTS

### System.String

## NOTES

## RELATED LINKS