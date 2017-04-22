- Ingresar a https://functions.azure.com/signin

<img src="https://bv8lsa-ch3302.files.1drv.com/y3m_tPMQc_2yD2QxUmgEA-Oq9bR9ZEzN7Km_D_-bejZc8sj4H-V5xFg3N1FPFvve1zvNokyPb0fVB_qCvReCeWAlGGf87JqVeallpq4rJpO0zIQI--oqckMlhZ7XQFtTNKusFuFKd9f7-BanU-bov3lin28kC0yVwKbrnDycg91FRs?width=925&amp;height=652&amp;cropmode=none">


```powershell
#Datos
$web = Invoke-WebRequest -Uri https://www.packtpub.com/packt/offers/free-learning -UseBasicParsing
$texto = ($web.RawContent -split '<div class="dotd-title">' | select -Last 1)
$title = (($texto -split '</h2>' | select -First 1) -split '<h2>' | select -Last 1).trim()
#Credenciales
$user = 'vmsilvamolina@victorsilva.com.uy'
$pass = (ConvertTo-SecureString 'XXXXXXXXXXXXXX' -AsPlainText -Force)
$cred = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $user, $pass
#Envío de mail 
$date = Get-Date -Format dd/MM
Send-MailMessage -To vmsilvamolina@gmail.com -From vmsilvamolina@victorsilva.com.uy -Subject "Packtpub: Libro gratis - $date" -Body $title -SmtpServer smtp.office365.com -UseSsl -Credential $cred -Port 587
```
