# Portal

### Iniciar sesión en el portal

- Navegar a la siguiente dirección URL: https://portal.azure.com e ingresar con las credenciales de nuestra suscripción.

### Crear el servidor SQL Server y el Grupo de Recursos

En el portal seleccionar New (+), ingresar SQL Data y seleccionar el resultado para desplegar el asistente:
<img src="https://do3riw-ch3302.files.1drv.com/y4mO87S7UzK-yn-buislkU_gUrd1YLCQtjlum_Oe8_QcQR4Jj-_oGaZKewALRj1Artl7z8rOjrqG9wXzdDP6mpT414cHmCtqkgrxhQPthhdHIrKmBEuowgcgjn8luPGqCQWo2Dv_FlTE09PJ0X_XUxpgBqlEUjtBmWYrPVrsamuOhrtldC_OGia7gPVnQrBcz8BVjWzEM5tRxMwpFLcKBY23g?width=397&height=266&cropmode=none">
Y luego *Create*, en la sección que aparece.

<img src="https://do3siw-ch3302.files.1drv.com/y4mR_XJZ-fq9vWlyuaKttEoDGhGg1wklkN4k97ml87P-Q8PlQ7sTYQ-kD-w7cyZcBBltHPyByt-beh5of6FoAJ99PCxfmkCklNlOl_2FHugP3HQBdiJYCFJii_l44FlAwNhsfsLzmVpI7lQTh3Qu095wXIsaDY1m3n1UWWlFG-Hjdf3ew0PbORTcXDIF_CZc7ZG3jQJBV0-0Nz8y2_gyf5DXw?width=1366&height=640&cropmode=none">

- Completar los siguientes campos con información relevante, como por ejemplo el nombre de la base de datos y en este caso, seleccionar el sample que permite utilizar Azure para crear una base con datos de ejemplo ya incorporados. También seleccionar si se utiliza un grupo de recursos existente o uno nuevo (al que se debe nombrar).

<img src="https://ce3siw-ch3302.files.1drv.com/y4mIle-eJhCUMg-u7dElqyrFjH3WLi66P9o0Sm5iLzJNFUBsfGUXFLjLz7yQpwcApYbf7Z_GC8HwMuFdbQJ6Ip8oVO2pIBI85xEyyI2jbIfT46jC9Yditvw7W8DCSQrrQSVwGMGrRWWKkOXJJHvDJOOjRxKULIA56zo3MN4Q5pYpQc7jsd1L_FTg_qDLFQs07NjYlbPZ_NkHC1BZr2evwUexA?width=639&height=357&cropmode=none">

- Seleccionar *Server* para continuar configurando las opciones necesarias. Dentro del menú que se desplegó ingresar el nombre del nuevo servidor de SQL, y el usuario administrador (nombre y contraseña), que vamos a generar para esta instancia. Por último, determinar en que región se va a ubicar nuestro nuevo servidor.

<img src="https://ce3riw-ch3302.files.1drv.com/y4mvEIygHt_f_aP1YH074qihnm5lpQWPa9Jp92scLKfS4af5H2ljCAvtDS5P6pmHGOAHIo32V9Nq3T63tIIXiLlN46a3y7Ro55OCKseEXZGAaz5fV_ZapMz-yLtmNxc8tlgMi3FK67IUUtYbE0NQMddWAAPYov84pGcYbHmO0lU9lXtEferIRwOabQNsZ9O7ZIO6I-pQHzcrnRLxLqEpCaEsw?width=1366&height=640&cropmode=none">

- En la opción *Pricing Tier*, seleccionar **Basic** y aplicar el cambio para no consumir de forma extendida la suscripción de prueba.

<img src="https://ce3qiw-ch3302.files.1drv.com/y4mCWL_G30enONY5WEsPKSKBLb6hjaCn1G88eNOD131DwIcJJQ5otXhyaYcCSy84RNvgJmt94TvhTUI8pG0DcuLMbUVuABqV_SPFAGBR-XmlPZCkbPNr5uixzKLCcAKFLwZ_UyZrgSM6ojIXq0tw0O8hdjCUQ1KhKx3-MdX0pBinKkFToMOC5qDErIfZzKVKnqjhEL4_5Fkqr61AuDLhPTWrA?width=1366&height=641&cropmode=none">

Y como último paso seleccionar *Create*.

### Habilitar acceso a nuestra IP


- Luego de generar la regla, clic en Ok.


### Conectar la Base de Datos

- Abrimos Visual Studio y seleccionamos *Server Explorer*, en la opción *Data Connection*, clic derecho y *Add Connection...*

<img>

- En la ventana desplegable seleccionamos *Microsoft SQL Server*

<img>

- En el campo *Server name* ingresamos el nombre de nuestro servidor generado pasos atrás junto al sufijo *.database.windows.net*, obteniendo como resultado:

> servername.database.windows.net




###


# Consola

## Instalar el módulo de Azure PowerShell 

```powershell
Install-Module -Name AzureRM -Scope CurrentUser -Force
```

## Iniciar sesión a nuestra suscripción de Azure

```powershell
Add-AzureRmAccount
```

## Create un Azure Resource Manager Resource Group

```powershell
$ResourceGroup = @{
    Name = 'AzureFunctions-SQL'
    Location = 'East US'
}
New-AzureRmResourceGroup @ResourceGroup
```
## Create an Azure SQL Server

```powershell
$SqlServer = @{
    ResourceGroupName = 'AzureFunctions-SQL'
    Name = 'mvdgabsqlvs'
    Location = 'East US'
    SqlAdministratorCredentials = (Get-Credential)
    ServerVersion = '12.0'
}
New-AzureRmSqlServer @SqlServer
```

## Create an Azure SQL Database

```powershell
$SqlDatabase = @{
    ResourceGroupName = 'AzureFunctions-SQL'
    ServerName = 'mvdgabsqlVS'
    DatabaseName = 'functionsworkshop'
    Edition = 'Basic'
}
New-AzureRmSqlDatabase @SqlDatabase
```
