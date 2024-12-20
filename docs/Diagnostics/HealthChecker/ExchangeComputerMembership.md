# Exchange Server Computer Membership

### Description:

Checks for the computer object to be members of the `Exchange Trusted Subsystem` and `Exchange Servers` security groups by default. It will also make sure the default local system account has the `Exchange Trusted Subsystem` a member of it as well in order to have the correct access to local system files.

This check is done by using the ADModule with using the cmdlets `Get-LocalGroupMember -SID "S-1-5-32-544"` and running `Get-ADPrincipalGroupMembership (Get-ADComputer $env:COMPUTERNAME).DistinguishedName`

If an issue is detected, the group will display with where the problem is located. Either `Local System Membership` if the group isn't part of the local system account or `AD Group Membership` if the computer object isn't a member of the group provided.

If the script is run from a computer that doesn't have Active Directory PowerShell module installed on it, `Get-ADComputer` will fail with the exception `CommandNotFoundException`. The output will then display that you should run `Install-WindowsFeature RSat-AD-PowerShell` on the computer to get the module installed. This is how you get this feature to then start reporting correctly.

**Included in HTML Report?**

Yes
