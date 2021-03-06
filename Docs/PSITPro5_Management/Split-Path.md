﻿# Split-Path

## SYNOPSIS
Returns the specified part of a path.

## DESCRIPTION
The Split-Path cmdlet returns only the specified part of a path, such as the parent directory, a child directory, or a file name.
It can also get items that are referenced by the split path and tell whether the path is relative or absolute.

You can use this cmdlet to get or submit only a selected part of a path.

## PARAMETERS

### Credential [PSCredential]

```powershell
[Parameter(ValueFromPipelineByPropertyName = $true)]
```

Specifies a user account that has permission to perform this action.
The default is the current user.

Type a user name, such as "User01" or "Domain01\User01".
Or, enter a PSCredential object, such as one generated by the Get-Credential cmdlet.
If you type a user name, you will be prompted for a password.

This parameter is not supported by any providers installed with Windows PowerShell.


### InformationAction [System.Management.Automation.ActionPreference]

```powershell
[ValidateSet(
  'SilentlyContinue',
  'Stop',
  'Continue',
  'Inquire',
  'Ignore',
  'Suspend')]
```


Type a user name, such as "User01" or "Domain01\User01".
Or, enter a PSCredential object, such as one generated by the Get-Credential cmdlet.
If you type a user name, you will be prompted for a password.

This parameter is not supported by any providers installed with Windows PowerShell.


### InformationVariable [System.String]


Type a user name, such as "User01" or "Domain01\User01".
Or, enter a PSCredential object, such as one generated by the Get-Credential cmdlet.
If you type a user name, you will be prompted for a password.

This parameter is not supported by any providers installed with Windows PowerShell.


### IsAbsolute [switch]

```powershell
[Parameter(ParameterSetName = 'Set 2')]
```

Returns TRUE ($True) if the path is absolute and FALSE ($False) if it is relative.
An absolute path has a length greater than zero and does not use a dot ( . ) to indicate the current path.


### Leaf [switch]

```powershell
[Parameter(
  ValueFromPipelineByPropertyName = $true,
  ParameterSetName = 'Set 3')]
```

Returns only the last item or container in the path.
For example, in the path "C:\Test\Logs\Pass1.log", it returns only "Pass1.log".


### LiteralPath [String[]]

```powershell
[Parameter(
  Mandatory = $true,
  ValueFromPipelineByPropertyName = $true,
  ParameterSetName = 'Set 4')]
```

Specifies the paths to be split.
Unlike Path, the value of LiteralPath is used exactly as it is typed.
No characters are interpreted as wildcards.
If the path includes escape characters, enclose it in single quotation marks.
Single quotation marks tell Windows PowerShell not to interpret any characters as escape sequences.


### NoQualifier [switch]

```powershell
[Parameter(
  ValueFromPipelineByPropertyName = $true,
  ParameterSetName = 'Set 5')]
```

Returns the path without the qualifier.
For the FileSystem or registry providers, the qualifier is the drive of the provider path, such as C: or HKCU:.
For example, in the path  "C:\Test\Logs\Pass1.log", it returns only "\Test\Logs\Pass1.log".


### Parent [switch]

```powershell
[Parameter(
  ValueFromPipelineByPropertyName = $true,
  ParameterSetName = 'Set 1')]
```

Returns only the parent containers of the item or of the container specified by the path.
For example, in the path "C:\Test\Logs\Pass1.log", it returns "C:\Test\Logs".
The Parent parameter is the default split location parameter.


### Path [String[]]

```powershell
[Parameter(
  Mandatory = $true,
  Position = 1,
  ValueFromPipeline = $true,
  ValueFromPipelineByPropertyName = $true,
  ParameterSetName = 'Set 1')]
[Parameter(
  Mandatory = $true,
  Position = 1,
  ValueFromPipeline = $true,
  ValueFromPipelineByPropertyName = $true,
  ParameterSetName = 'Set 2')]
[Parameter(
  Mandatory = $true,
  Position = 1,
  ValueFromPipeline = $true,
  ValueFromPipelineByPropertyName = $true,
  ParameterSetName = 'Set 3')]
[Parameter(
  Mandatory = $true,
  Position = 1,
  ValueFromPipeline = $true,
  ValueFromPipelineByPropertyName = $true,
  ParameterSetName = 'Set 5')]
[Parameter(
  Mandatory = $true,
  Position = 1,
  ValueFromPipeline = $true,
  ValueFromPipelineByPropertyName = $true,
  ParameterSetName = 'Set 6')]
```

Specifies the paths to be split.
Wildcards are permitted.
If the path includes spaces, enclose it in quotation marks.
You can also pipe a path to Split-Path.


### Qualifier [switch]

```powershell
[Parameter(
  Position = 2,
  ValueFromPipelineByPropertyName = $true,
  ParameterSetName = 'Set 6')]
```

Returns only the qualifier of the specified path.
For the FileSystem or registry providers, the qualifier is the drive of the provider path, such as C: or HKCU:.


### Resolve [switch]

Displays the items that are referenced by the resulting split path instead of displaying the path elements.


### UseTransaction [switch]

Includes the command in the active transaction.
This parameter is valid only when a transaction is in progress.
For more information, see Includes the command in the active transaction.
This parameter is valid only when a transaction is in progress.
For more information, see



## INPUTS
### System.String

You can pipe a string that contains a path to Split-Path.

## OUTPUTS
### System.String, System.Boolean

The Split-Path cmdlet returns text strings.
When you use the Resolve parameter, Split-Path returns a string that describes the location of the items; it does not return objects that represent the items, such as a FileInfo or RegistryKey object.

When you use the IsAbsolute parameter, Split-Path returns a Boolean value.

## NOTES
The split location parameters (Qualifier, Parent, Leaf, and NoQualifier) are exclusive.
You can use only one in each command.

The cmdlets that contain the Path noun (the Path cmdlets) manipulate path names and return the names in a concise format that all Windows PowerShell providers can interpret.
They are designed for use in programs and scripts where you want to display all or part of a path name in a particular format.
Use them like you would use Dirname, Normpath, Realpath, Join, or other path manipulators.

You can use the Path cmdlets with several providers, including the FileSystem, Registry, and Certificate providers.

The Split-Path cmdlet is designed to work with the data exposed by any provider.
To list the providers available in your session, type "Get-PSProvider".
For more information, see about_Providers.


## EXAMPLES
### -------------------------- EXAMPLE 1 --------------------------

```powershell
PS C:\>split-path "HKCU:\Software\Microsoft" -qualifier
HKCU:

```
This command returns only the qualifier (the drive) of the path.






### -------------------------- EXAMPLE 2 --------------------------

```powershell
PS C:\>split-path "C:\Test\Logs\*.log" -leaf -resolve
Pass1.log
Pass2.log
...

```
This command displays the files that are referenced by the split path.
Because this path is split to the last item (the "leaf"), only the file names of the paths are displayed.

The Resolve parameter tells Split-Path to display the items that the split path references, instead of displaying the split path.

Like all Split-Path commands, this command returns strings.
It does not return FileInfo Objects representing the files.






### -------------------------- EXAMPLE 3 --------------------------

```powershell
PS C:\>split-path "C:\WINDOWS\system32\WindowsPowerShell\V1.0\about_*.txt"
C:\WINDOWS\system32\WindowsPowerShell\V1.0

```
This command returns only the parent containers of the path.
Because it does not include any parameters to specify the split, Split-Path uses the split location default, which is Parent.






### -------------------------- EXAMPLE 4 --------------------------

```powershell
PS C:\>split-path ".\My Pictures\*.jpg" -IsAbsolute
False

```
This command determines whether the path is relative or absolute.
In this case, because the path is relative to the current directory, which is represented by a dot (.), it returns FALSE ($false).






### -------------------------- EXAMPLE 5 --------------------------

```powershell
PS C:\>set-location (split-path $profile)
PS C:\Documents and Settings\User01\My Documents\WindowsPowerShell>

```
This command changes your location to the directory that contains the Windows PowerShell profile.

The command in parentheses uses the Split-Path cmdlet to return only the parent of the path stored in the built-in $Profile variable. (The Parent parameter is the default split location parameter, so you can omit it from the command.) The parentheses direct Windows PowerShell to run the command first.
This is a handy way to navigate to a directory with a long path name.






### -------------------------- EXAMPLE 6 --------------------------

```powershell
PS C:\>'C:\Documents and Settings\User01\My Documents\My Pictures' | split-path
C:\Documents and Settings\User01\My Documents

```
This command uses a pipeline operator (|) to send a path to the Split-Path cmdlet.
The path is enclosed in quotation marks to indicate that it is a single token.







## RELATED LINKS

[Online Version:](http://go.microsoft.com/fwlink/p/?linkid=293917)

[Convert-Path]()

[Join-Path]()

[Resolve-Path]()

[Test-Path]()

[about_Providers]()

