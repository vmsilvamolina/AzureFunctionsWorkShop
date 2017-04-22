# Portal

## Iniciar sesión en el portal

Navegar a la siguiente dirección URL: https://portal.azure.com e ingresar con las credenciales de nuestra suscripción.

### Crear el servidor SQL Server y el Grupo de Recursos

En el portal seleccionar New (+), ingresar SQL Data y seleccionar el resultado para desplegar el asistente:

<img src="https://do3riw-ch3302.files.1drv.com/y4mO87S7UzK-yn-buislkU_gUrd1YLCQtjlum_Oe8_QcQR4Jj-_oGaZKewALRj1Artl7z8rOjrqG9wXzdDP6mpT414cHmCtqkgrxhQPthhdHIrKmBEuowgcgjn8luPGqCQWo2Dv_FlTE09PJ0X_XUxpgBqlEUjtBmWYrPVrsamuOhrtldC_OGia7gPVnQrBcz8BVjWzEM5tRxMwpFLcKBY23g?width=397&height=266&cropmode=none">

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
    Location = 'West US'
}
New-AzureRmResourceGroup @ResourceGroup
```
## Create an Azure SQL Server

```powershell
$SqlServer = @{
    ResourceGroupName = 'AzureFunctions-SQL'
    Name = 'mvdgabsqlVS'
    Location = 'West US'
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

## Conectarnos a la base de datos
