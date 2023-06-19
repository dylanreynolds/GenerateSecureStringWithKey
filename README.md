# GenerateSecureStringWithKey
Required for Local User Account creation, machine agnostic key and pwd file to be used in scripts.  Ensure your key is securely stored and called when using.

# .DESCRIPTION 

Creates a local admin using credentials key and secure key password txt file. (no stored text)

# .CREDIT 

Get-SecurePassword - credit to Author: Shawn Melton (@wsmelton)

# .INSTRUCTIONS
# (1) Create our key file
<code> New-KeyFile -KeyFile .\MyKey.key -KeySize 16 <code>
# (2) Create our password file
<code> New-PasswordFile -PwdFile .\MyPwd.txt -Key (Get-Content .\MyKey.key) <code>
# (3) Pull in the password to use
<code>$pwd = Get-SecurePassword -PwdFile .\MyPwd.txt -KeyFile .\MyKey.key <code>
 
# build the PSCredential object
<code> $mycred = New-Object System.Management.Automation.PSCredential("admin",$pwd) <code>
 
# show the password was captured
<code> $mycred.GetNetworkCredential().Password <code>
