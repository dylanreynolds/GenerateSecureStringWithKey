# GenerateSecureStringWithKey
Required for Local User Account creation, machine agnostic key and pwd file to be used in scripts.  Ensure your key is securely stored and called when using.

# .DESCRIPTION 

Creates a local admin using credentials key and secure key password txt file. (no stored text)

# .CREDIT 

Get-SecurePassword - credit to Author: Shawn Melton (@wsmelton)

# .INSTRUCTIONS
# (1) Create our key file
New-KeyFile -KeyFile .\MyKey.key -KeySize 16
# (2) Create our password file
New-PasswordFile -PwdFile .\MyPwd.txt -Key (Get-Content .\MyKey.key)
# (3) Pull in the password to use
$pwd = Get-SecurePassword -PwdFile .\MyPwd.txt -KeyFile .\MyKey.key
 
# build the PSCredential object
$mycred = New-Object System.Management.Automation.PSCredential("admin",$pwd)
 
# show the password was captured
$mycred.GetNetworkCredential().Password
