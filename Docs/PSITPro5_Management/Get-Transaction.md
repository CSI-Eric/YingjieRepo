﻿# Get-Transaction

## SYNOPSIS
Gets the current (active) transaction.

## DESCRIPTION
The Get-Transaction cmdlet gets an object that represents the current transaction in the session.

This cmdlet never returns more than one object, because only one transaction is active at a time.
If you start one or more independent transactions (by using the Independent parameter of Start-Transaction), the most recently started transaction is active, and that is the transaction that Get-Transaction returns.

When all active transactions have either been rolled back or committed, Get-Transaction shows the transaction that was most recently active in the session.

The Get-Transaction cmdlet is one of a set of cmdlets that support the transactions feature in Windows PowerShell.
For more information, see about_Transactions.

## PARAMETERS

### InformationAction [System.Management.Automation.ActionPreference]

```powershell
[Parameter(ParameterSetName = 'Set 1')]
[ValidateSet(
  'SilentlyContinue',
  'Stop',
  'Continue',
  'Inquire',
  'Ignore',
  'Suspend')]
```




### InformationVariable [System.String]

```powershell
[Parameter(ParameterSetName = 'Set 1')]
```





## INPUTS
### None

You cannot pipe objects to this cmdlet.

## OUTPUTS
### System.Management.Automation.PSTransaction

Get-Transaction returns an object that represents the current transaction.


## EXAMPLES
### -------------------------- EXAMPLE 1 --------------------------

```powershell
PS C:\>start-transaction
PS C:\>get-transaction

RollbackPreference   SubscriberCount   Status
------------------   ---------------   ------
Error                1                 Active

```
This command uses the Get-Transaction cmdlet to get the current transaction.






### -------------------------- EXAMPLE 2 --------------------------

```powershell
PS C:\>get-transaction | get-member

Name               MemberType Definition
----               ---------- ----------
Dispose            Method     System.Void Dispose(), System.Void Dispose(Boolean disposing)
Equals             Method     System.Boolean Equals(Object obj)
GetHashCode        Method     System.Int32 GetHashCode()
GetType            Method     System.Type GetType()
ToString           Method     System.String ToString()
IsCommitted        Property   System.Boolean IsCommitted {get;}
IsRolledBack       Property   System.Boolean IsRolledBack {get;}
RollbackPreference Property   System.Management.Automation.RollbackSeverity RollbackPreference {get;}
SubscriberCount    Property   System.Int32 SubscriberCount {get;set;}

```
This command uses the Get-Member cmdlet to show the properties and methods of the transaction object.






### -------------------------- EXAMPLE 3 --------------------------

```powershell
PS C:\>cd hklm:\software
HKLM:\SOFTWARE> Start-Transaction
HKLM:\SOFTWARE> New-Item MyCompany -UseTransaction
HKLM:\SOFTWARE> Undo-Transaction
HKLM:\SOFTWARE> Get-Transaction

RollbackPreference   SubscriberCount   Status
------------------   ---------------   ----------
Error                0                 RolledBack

```
This command shows the property values of a transaction object for a transaction that has been rolled back.






### -------------------------- EXAMPLE 4 --------------------------

```powershell
PS C:\>cd hklm:\software
HKLM:\SOFTWARE> Start-Transaction
HKLM:\SOFTWARE> New-Item MyCompany -UseTransaction
HKLM:\SOFTWARE> Complete-Transaction
HKLM:\SOFTWARE> Get-Transaction

RollbackPreference   SubscriberCount   Status
------------------   ---------------   ---------
Error                1                 Committed

```
This command shows the property values of a transaction object for a transaction that has been committed.






### -------------------------- EXAMPLE 5 --------------------------

```powershell
PS C:\>cd hklm:\software
HKLM:\SOFTWARE> Start-Transaction
HKLM:\SOFTWARE> New-Item MyCompany -UseTransaction
HKLM:\SOFTWARE> Start-Transaction
HKLM:\SOFTWARE> New-Item MyCompany2 -UseTransaction
HKLM:\SOFTWARE> Get-Transaction

RollbackPreference   SubscriberCount   Status
------------------   ---------------   ------
Error                2                 Active

HKLM:\SOFTWARE> Complete-Transaction
HKLM:\SOFTWARE> Get-Transaction

RollbackPreference   SubscriberCount   Status
------------------   ---------------   ------
Error                1                 Active

HKLM:\SOFTWARE> Complete-Transaction
HKLM:\SOFTWARE> Get-Transaction

RollbackPreference   SubscriberCount   Status
------------------   ---------------   ---------
Error                1                 Committed

```
This example shows the effect on the transaction object of starting a transaction while another transaction is in progress.
Typically, this happens when a script that runs a transaction includes a function or calls a script that contains another complete transaction.

Unless the second Start-Transaction command includes the Independent parameter, Start-Transaction does not create a new transaction.
Instead, it adds a second subscriber to the original transaction.

The first Start-Transaction command starts the transaction.
A New-Item command with the UseTransaction parameter is part of the transaction.

A second Start-Transaction command adds a subscriber to the transaction.
The next New-Item command is also part of the transaction.

The first Get-Transaction command shows the multi-subscriber transaction.
Notice that the subscriber count is 2.

The first Complete-Transaction command does not commit the transaction, but it reduces the subscriber count to 1.

The second Complete-Transaction command commits the transaction.






### -------------------------- EXAMPLE 6 --------------------------

```powershell
PS C:\>HKLM:\SOFTWARE> Start-Transaction
HKLM:\SOFTWARE> Get-Transaction

RollbackPreference   SubscriberCount   IsRolledBack   IsCommitted
------------------   ---------------   ------------   -----------
Error                1                 False          False

HKLM:\SOFTWARE> Start-Transaction -Independent
HKLM:\SOFTWARE> Get-Transaction

RollbackPreference   SubscriberCount   IsRolledBack   IsCommitted
------------------   ---------------   ------------   -----------
Error                1                 False          False

HKLM:\SOFTWARE> Complete-Transaction
HKLM:\SOFTWARE> Get-Transaction
HKLM:\SOFTWARE> Complete-Transaction
HKLM:\SOFTWARE> Get-Transaction

```
This example shows the effect on the transaction object of starting an independent transaction while another transaction is in progress.

The first Start-Transaction command starts the transaction.
A New-Item command with the UseTransaction parameter is part of the transaction.

A second Start-Transaction command adds a subscriber to the transaction.
The next New-Item command is also part of the transaction.

The first Get-Transaction command shows the multi-subscriber transaction.
Note that the subscriber count is 2.

The Complete-Transaction command reduces the subscriber count to 1, but it does not commit the transaction.

The second Complete-Transaction command commits the transaction.







## RELATED LINKS

[Online Version:](http://go.microsoft.com/fwlink/p/?linkid=290504)

[Complete-Transaction]()

[Start-Transaction]()

[Undo-Transaction]()

[Use-Transaction]()

[about_Providers]()

[about_Transactions]()

