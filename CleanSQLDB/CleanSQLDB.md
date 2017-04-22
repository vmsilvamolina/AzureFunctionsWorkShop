# Modificar registros en base de datos SQL

Esta segunda parte del WorkShop, vamos a ver como podemos acceder a nuestra base de datos para realizar acciones, ya sean de administración así como también de mantenimiento de la misma.

#### Iniciar sesión en el portal

- Navegar a la siguiente dirección URL: https://portal.azure.com e ingresar con las credenciales de nuestra suscripción.

#### Crear el servidor SQL Server y el Grupo de Recursos

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

#### Habilitar acceso a nuestra IP

- Para poder acceder a las bases de datos de un servidor de Azure SQL debemos crear una regla en el Firewall, para ello vamos a nuestro grupo de recursos, seleccionamos el servidor de SQL y luego seleccionamos *Firewall*:

<img src="https://ce3oiw-ch3302.files.1drv.com/y4mSVmeLGH5pTugsJnw39FfYmGiw26Ynhez4OA595cHIDwItmbMdeUYP0tYooXxC583Xk2X_jwh2q7HkNPlVBXL4_kStsCL0_e8JLghPLcE657pX_R-htjRZilz70i1dbEwCQExokCBHRYF5Ug5erU6yOG-sxhEG25N0YLbfbjAST3GKDSwarejyNYakk-wJ1ugt3X_z7W8-VQvYGrgRKvZMw?width=1366&height=640&cropmode=none">

- En la imagen se detalla la regla de modo que permita el acceso desde cualquier IP (menos seguro, solamente para el ejemplo). Clic en *Save* para guardar cambios. Luego de generar la regla, clic en Ok.


#### Conectar la Base de Datos

- Abrimos Visual Studio y seleccionamos *Server Explorer*, en la opción *Data Connection*, clic derecho y *Add Connection...*

<img src="https://ce3piw-ch3302.files.1drv.com/y4m9FSRELAn0taIISK03UTmNIxYHLL_E-7WCIZXrzRXxPC3HSRPJTtGtTIVspbfJP86o8zhmVkoOMJbz-GTuzFXSHqmd7D7vNyY1UbkfQE7fKYub4b1cQIfbdIB4FsuEl_HpulRcY7miQj4dTU6f_DscRMoInpkAblRkn50nSWoNDQiiI14TYfG6e4kWMPRTYRzSPkhXMTZuR1iEOhOuFRwgg?width=497&height=298&cropmode=none">

- En la ventana desplegable seleccionamos *Microsoft SQL Server*

<img src="https://ce3niw-ch3302.files.1drv.com/y4mTtDBywel31QD4DWvWeo2LPhMC3_E0tbNSZ7VgeE7YL8fc9SvFhFsQDsprL2p58__tsODc-fR7OMT0dvRz05FLjWrJUEL3Qi8gLa9GXUmIBtJwjjgBBvjlBXDYiA2vZUJlO0yqhus9pG6ykyQ1PIDKJ_8oEe06n2WixxWA1l8myGkjazjS3czQI6isIIVACeEVL3wNmmyJcFZt_sGwLWUBw?width=554&height=654&cropmode=none">

- En el campo *Server name* ingresamos el nombre de nuestro servidor generado pasos atrás junto al sufijo *.database.windows.net*, obteniendo como resultado:

> servername.database.windows.net

#### Crear la función para limpiar registros

- Antes de comenzar con la función, para poder acceder a nuestra base de datos desde Azure Functions, vamos a necesitar el string de conexión. Para ello, accedemos a las propiedades de la base de datos y seleccionamos el string y modificamos los valores de conexión según los datos del usuario y contraseña definidos:

<img src="https://dp3miw-ch3302.files.1drv.com/y4mi5k7CRN1w2S6BgOPm2DbYovPXwTeABshmdLfgarvwmF1bZXkM6WyFyuaPcp4x1V98dCMt1RNC2au3gVchpWl5Ie6E4t1QVkd1dhTI5V1dJxKkJ6U9RnE7oe-EjfLPDpBR5yGJnWSJUNAee1QB7MtouHfjZRg5YIfeleJ2MholiyuFURkaBvSW7xXQAOy6fBAOgvYBJuV6WtWhnM4cASIBw?width=1366&height=641&cropmode=none">

<img src="https://dp3niw-ch3302.files.1drv.com/y4mLJWJarA4YTmCgoe4BO_eRPybnV_Le8HeS_UX023vC05ynuySdzDmt4xXL2m8hgqO0EbfzxuPerQ5z_TwWkyziauqUKWqmF8MIP2L_rEt3SvDadvzq5F7pSeaW9bKb_A3v62OitutsQ3xMS97VHQ6WbT9Ri3tIpua0Q_F-5Zamz3y0DeX_szxy9dpuCBkcOYVc_BUoIxe7PoyhlQjxbsOyw?width=572&height=514&cropmode=none">

Seleccionamos el string completo teniendo en cuenta que debemos modificar los datos de accesos (ingresar el username y password) dentro de la cadena:

```
Server=tcp:mvdgabsqlvs.database.windows.net,1433;Initial Catalog=functionsworkshop;Persist Security Info=False;User ID='{sql_username}';Password='{sql_password}';MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;
```

Ya con el string de conexión, vamos a generar la función. Desde el portal vamos a acceder al siguiente enlace: https://functions.azure.com/signin para comenzar a crear nuestra función. Ingresamos el nuevo nombre de la función y la región a crear:

<img src="https://dp3oiw-ch3302.files.1drv.com/y4mgI3TTKYyCIB5zNXroZ6HYXjMx0-vuYwgRkT3LloUoOmlBt7ebO5YcMo5NIH3YPZW29SUTgdqLhrdVEYplTZkt1dVK6YpdM8JIURBVXkRyWSK0O4bthY6-Ff-8-D-HSNEaGUZ1pua_D8x8h1_WMz7ID6miXT6f2n2Jf3DZI_kSfHk5mmTLjOB0Bvg8WC_B-nyn2_UZk06AUFXmSQamRLiGA?width=1355&height=517&cropmode=none">

Clic en *Create + Get started*


- Con la Function App creada, el siguiente paso es crear la función como indica la siguiente imagen:

<img src="https://eo3miw-ch3302.files.1drv.com/y4mWTOJwF8fQ66_ZL2xIuw4UKaFC7KSYa9u4oG8FpxUDhRRXjeGVAg3VyeOCfUGq_xIP6ofFOCTsKfKbWpYiqpEIJa_U8FJJ0e6u7adGiSRKULj1845xqSIHEopW_z4S6WgL362WCik7-GL3QUVpaSZ7mXIbPIp9QkoShte8qLsVwKeRMykAx4R5z0zjnIHFwnMDuB9caBI6yf-a56vPzL9Ww?width=1355&height=585&cropmode=none">

Seleccionar ***create your own custom function*** y dentro de las opciones que aparecen hacer clic en **TimerTrigger-CSharp**.

<img src="https://eo3niw-ch3302.files.1drv.com/y4meqkCefxGPPLRjUj47iCBB66kiOKtllpI0mdxjdF9-FNidLmM_T6t1zAdCU8WsKyN6jSpyx1BdWtdA9mREUHQFhU79tz0lQDunnyT8yPwrLoOle_KclD8MSDCtbl4EQqRAToSa0cFQl79LRZwlJDWlHCZ228WTjVjaquD4rXviSaIJM1s2ZPqG4jh3z6gvVbnqqZZhJKKqQzPv4CGSwE4ow?width=1036&height=477&cropmode=none">

E ingresar el nombre de la función y la región donde se va a crear:

<img src="https://eo3oiw-ch3302.files.1drv.com/y4m84gUGV1WG6OOwSRjl3H9F_gxgoDE-aGGwUwzNJApAzNfJngBYwkLmvyV0ckfljekt-UgZQXUFN0IgAe8eaMUo3RgqutXOWkvKbrzwI0uNUxsspQOH9CAVrIyR0Id99ubfQ7CnA0Pd7tFsDItpKmZI4JPVHrJTMzkVEC5gB47AfdNWSQvXKZylI0qAva0jeSnzPg6b_QpNHz9tHodC_pp9g?width=337&height=322&cropmode=none">


Ahora que se encuentra creada la función en pantalla tenemos un fragmento de código que vamos a reemplazar por lo siguiente:

```csharp
#r "System.Configuration"
#r "System.Data"

using System;

using System.Configuration;
using System.Data.SqlClient;
using System.Threading.Tasks;

public static async Task Run(TimerInfo myTimer, TraceWriter log)
     {
         var str = ConfigurationManager.ConnectionStrings["sqldb_connection"].ConnectionString;
         using (SqlConnection conn = new SqlConnection(str))
         {
             conn.Open();
             // Reemplazo valores
             var text = "UPDATE SalesLT.Address SET City = 'Montevideo' Where City = 'Toronto'";
             using (SqlCommand cmd = new SqlCommand(text, conn))
             // Imprimo un log en pantalla
             log.Info($"Listo!");
         }
     }
```

Y que permite realizar el código anterior? Permite modificar los registros de la tabla SalesLT.Address dentro de la columna City sean modificados (de pasar a ser Toronto a Montevideo).

Con el ejemplo anterior tenemos de forma programada una función que permite realizar acciones en nuestra base de datos, de forma automática sin tener que ocuparnos en dónde corre o que necesito para ejecutarla.