﻿# Set-Content

## SYNOPSIS
Writes or replaces the content in an item with new content.

## DESCRIPTION
The Set-Content cmdlet is a string-processing cmdlet that writes or replaces the content in the specified item, such as a file.
Whereas the Add-Content cmdlet appends content to a file, Set-Content replaces the existing content.
You can type the content in the command or send content through the pipeline to Set-Content.

## PARAMETERS

### Credential [PSCredential]

```powershell
[Parameter(ValueFromPipelineByPropertyName = $true)]
```

Specifies a user account that has permission to perform this action.
The default is the current user.

Type a user name, such as "User01" or "Domain01\User01", or enter a PSCredential object, such as one generated by the Get-Credential cmdlet.
If you type a user name, you will be prompted for a password.

This parameter is not supported by any providers installed with Windows PowerShell.


### Encoding [Microsoft.PowerShell.Commands.FileSystemCmdletProviderEncodingal]

```powershell
[ValidateSet(
  'Unknown',
  'String',
  'Unicode',
  'Byte',
  'BigEndianUnicode',
  'UTF8',
  'UTF7',
  'UTF32',
  'Ascii',
  'Default',
  'Oem',
  'BigEndianUTF32')]
```


Type a user name, such as "User01" or "Domain01\User01", or enter a PSCredential object, such as one generated by the Get-Credential cmdlet.
If you type a user name, you will be prompted for a password.

This parameter is not supported by any providers installed with Windows PowerShell.


### Exclude [String[]]

Omits the specified items.
The value of this parameter qualifies the Path parameter.
Enter a path element or pattern, such as "*.txt".
Wildcards are permitted.


### Filter [String]

Specifies a filter in the provider's format or language.
The value of this parameter qualifies the Path parameter.
The syntax of the filter, including the use of wildcards, depends on the provider.
Filters are more efficient than other parameters, because the provider applies them when retrieving the objects, rather than having Windows PowerShell filter the objects after they are retrieved.


### Force [switch]

Allows the cmdlet to set the contents of a file, even if the file is read-only.
Implementation varies from provider to provider.
For more information, see about_Providers.
Even using the Force parameter, the cmdlet cannot override security restrictions.


### Include [String[]]

Changes only the specified items.
The value of this parameter qualifies the Path parameter.
Enter a path element or pattern, such as "*.txt".
Wildcards are permitted.


### InformationAction [System.Management.Automation.ActionPreferenceal]

```powershell
[ValidateSet(
  'SilentlyContinue',
  'Stop',
  'Continue',
  'Inquire',
  'Ignore',
  'Suspend')]
```


Type a user name, such as "User01" or "Domain01\User01", or enter a PSCredential object, such as one generated by the Get-Credential cmdlet.
If you type a user name, you will be prompted for a password.

This parameter is not supported by any providers installed with Windows PowerShell.


### InformationVariable [System.Stringal]


Type a user name, such as "User01" or "Domain01\User01", or enter a PSCredential object, such as one generated by the Get-Credential cmdlet.
If you type a user name, you will be prompted for a password.

This parameter is not supported by any providers installed with Windows PowerShell.


### LiteralPath [String[]]

```powershell
[Parameter(
  Mandatory = $true,
  ParameterSetName = 'Set 2')]
```

Specifies the path to the item that will receive the content.
Unlike Path, the value of LiteralPath is used exactly as it is typed.
No characters are interpreted as wildcards.
If the path includes escape characters, enclose it in single quotation marks.
Single quotation marks tell Windows PowerShell not to interpret any characters as escape sequences.


### PassThru [switch]

Returns an object representing the content.
By default, this cmdlet does not generate any output.


### Path [String[]]

```powershell
[Parameter(
  Mandatory = $true,
  Position = 1,
  ValueFromPipelineByPropertyName = $true,
  ParameterSetName = 'Set 1')]
```

Specifies the path to the item that will receive the content.
Wildcards are permitted.


### Stream [System.Stringal]


Type a user name, such as "User01" or "Domain01\User01", or enter a PSCredential object, such as one generated by the Get-Credential cmdlet.
If you type a user name, you will be prompted for a password.

This parameter is not supported by any providers installed with Windows PowerShell.


### Value [Object[]]

```powershell
[Parameter(
  Mandatory = $true,
  Position = 2,
  ValueFromPipeline = $true,
  ValueFromPipelineByPropertyName = $true)]
```

Specifies the new content for the item.


### Confirm [switch]

Prompts you for confirmation before running the cmdlet.Prompts you for confirmation before running the cmdlet.


### WhatIf [switch]

Shows what would happen if the cmdlet runs.
The cmdlet is not run.Shows what would happen if the cmdlet runs.
The cmdlet is not run.


### UseTransaction [switch]

Includes the command in the active transaction.
This parameter is valid only when a transaction is in progress.
For more information, see Includes the command in the active transaction.
This parameter is valid only when a transaction is in progress.
For more information, see



## INPUTS
### System.Object

You can pipe an object that contains the new value for the item to Set-Content.

## OUTPUTS
### None or System.String

When you use the Passthru parameter, Set-Content generates a System.String object representing the content.
Otherwise, this cmdlet does not generate any output.

## NOTES
You can also refer to Set-Content by its built-in alias, "sc".
For more information, see about_Aliases.

Set-Content is designed for string processing.
If you pipe non-string objects to Set-Content, it converts the object to a string before writing it.
To write objects to files, use Out-File.

The Set-Content cmdlet is designed to work with the data exposed by any provider.
To list the providers available in your session, type "Get-PsProvider".
For more information, see about_Providers.


## EXAMPLES
### -------------------------- EXAMPLE 1 --------------------------

```powershell
PS C:\>set-content -path C:\Test1\test*.txt -value "Hello, World"

```
This command replaces the contents of all files in the Test1 directory that have names beginning with "test" with "Hello, World".
This example shows how to specify content by typing it in the command.






### -------------------------- EXAMPLE 2 --------------------------

```powershell
PS C:\>get-date | set-content C:\Test1\date.csv

```
This command creates a comma-separated variable-length (csv) file that contains only the current date and time.
It uses the Get-Date cmdlet to get the current system date and time.
The pipeline operator passes the result to Set-Content, which creates the file and writes the content.

If the Test1 directory does not exist, the command fails, but if the file does not exist, the command will create it.






### -------------------------- EXAMPLE 3 --------------------------

```powershell
PS C:\>(get-content Notice.txt) | foreach-object {$_ -replace "Warning", "Caution"} | set-content Notice.txt

```
This command replaces all instances of "Warning" with "Caution" in the Notice.txt file.

It uses the Get-Content cmdlet to get the content of Notice.txt.
The pipeline operator sends the results to the ForEach-Object cmdlet, which applies the expression to each line of content in Get-Content.
The expression uses the "$_" symbol to refer to the current item and the Replace parameter to specify the text to be replaced.

Another pipeline operator sends the changed content to Set-Content which replaces the text in Notice.txt with the new content.

The parentheses around the Get-Content command ensure that the Get operation is complete before the Set operation begins.
Without them, the command will fail because the two functions will be trying to access the same file.







## RELATED LINKS

[Online Version:](http://go.microsoft.com/fwlink/p/?linkid=293909)

[Add-Content]()

[Clear-Content]()

[Get-Content]()

[about_Providers]()

