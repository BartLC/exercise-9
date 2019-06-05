New-ADUser -name "Voornaam Achternaam" -AccountPassword '
(ConvertTo-SecureString -AsPlainText "#Geheim" -Force) '
-DisplayName "Voornaam Achternaam" '
-SamAccountName "achternaam" '
-Enabeld $true

$users = Import-Csv -Delimiter ";" -path C:\Import_ADUsers.csv
ForEach ($user in $users)
{
$fullname = $user.firstname + " " + $user.lastname
$firstname = $user.firstname
$lastname = $user.lastname
$domain = "mediatech.lan"
$upn = $user.lastname + $domain
$ou = $user.ou
$password = $user.password
$driveletter = "C:"
$homefolder = $user.homefolder
$setpassword = ConvertTo-SecureString $password -AsPlainText -Force
}

New-ADUser -Name $fullname -DisplayName $fullname '
-GivenName $firstname -surname $lastname '
-SamAccountName $user.lastname -HomeDrive $driveletter '
-HomeDirectory $homefolder -UserPrincipalName $upn -Path $ou '
-AccountPassword $setpassword -Enabeld $true -PassThru
