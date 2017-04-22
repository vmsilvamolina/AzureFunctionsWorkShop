#### Iniciar sesión en el portal

- Ingresar a https://functions.azure.com/signin

- Habiendo iniciado sesión en el portal lo siguiente es nombrar nuestra futura función e ingresar la región dondes será creada:
<img src="https://bv8lsa-ch3302.files.1drv.com/y3m_tPMQc_2yD2QxUmgEA-Oq9bR9ZEzN7Km_D_-bejZc8sj4H-V5xFg3N1FPFvve1zvNokyPb0fVB_qCvReCeWAlGGf87JqVeallpq4rJpO0zIQI--oqckMlhZ7XQFtTNKusFuFKd9f7-BanU-bov3lin28kC0yVwKbrnDycg91FRs?width=925&amp;height=652&amp;cropmode=none">

- Teniendo la function app creada, vamos a generar una Función del tipo *TimerTrigger-PowerShell*:

<img src="https://bv8nsa-ch3302.files.1drv.com/y3m-3jzL9oQPtnBQlmlhm1hqNcqlMohnu4bNHs1EdLC99x8SaULxN0MQTamO9-SH6Pq5ZgvCMnXZskMvhM0Z-yJj0MkSLdbVDUInNz7KeROkTG7Y4ATpqB4L_XP1IgC9bm_ym9Cme6ioMqNrvwEJgd4KVwgXTrrnuufb49Q5NvtHJY?width=1166&height=573&cropmode=none">

#### Scheduler

- Posteriormente debemos seleccionar la periodicidad en la que se va a ejecutar nuestra función. Azure Functions utiliza expresiones CRON para planificar la ejecución de nuestra función. No pretendo profundizar sobre como funciona pero básicamente debemos tener clara la estructura que es la siguiente:


```
{second} {minute} {hour} {day} {month} {day of the week}
```

Un ejemplo de uso sería el siguiente:

- Para ejecutar todos los días a las 10:00hs (en horario UTC-3:00) debemos ingresar lo siguiente:

>0 0 13 * * *

#### Código

Como se comenzó al principio vamos a reemplazar el código con el siguiente fragmento de PowerShell para poder realizar nuestro objetivo:

```powershell
#Datos
$web = Invoke-WebRequest -Uri https://www.packtpub.com/packt/offers/free-learning -UseBasicParsing
$texto = ($web.RawContent -split '<div class="dotd-title">' | select -Last 1)
$title = (($texto -split '</h2>' | select -First 1) -split '<h2>' | select -Last 1).trim()
#Credenciales
$user = 'mailpersonal@dominio.com'
$pass = (ConvertTo-SecureString 'P@ssw0rd' -AsPlainText -Force)
$cred = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList $user, $pass
#Envío de mail 
$date = Get-Date -Format dd/MM
Send-MailMessage -To vmsilvamolina@gmail.com -From vmsilvamolina@victorsilva.com.uy -Subject "Packtpub: Libro gratis - $date" -Body $title -SmtpServer smtp.office365.com -UseSsl -Credential $cred -Port 587
```

- Ya con el código ingresado, vamos a guardar los cambios y como último paso a ejecutar, para poder obtener como resultado nuestro mail con la información del título del libro sin necesidad de acceder a la página, utilizando una función simple en Azure y de forma automática.