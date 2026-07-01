Para transformar este documento en un manual técnico de ingeniería de alta fidelidad para el examen AZ-104, es crucial inyectar tres precisiones mecánicas del plano de control que Microsoft evalúa con rigor:

Contenido Oficial Requerido (AZ-104)
1. El concepto de Contexto de Azure (AzureRmContext)
En tu sección sobre Subscription Management, mencionas el uso de Set-AzContext. Para el examen, debes profundizar en qué es exactamente un Contexto en Azure PowerShell, ya que es la estructura de datos que evita la pérdida de estado entre ejecuciones:

La Composición: Un contexto de Azure (PSAzureContext) es un objeto en memoria que consolida tres elementos clave: el Usuario/Service Principal autenticado, la Suscripción activa y el Inquilino (Tenant ID) de Microsoft Entra.

El parámetro -AzContext: Muchos cmdlets avanzados del módulo Az aceptan el parámetro ejecutor -AzContext. Esto permite a un script de automatización realizar operaciones en múltiples suscripciones de manera simultánea en hilos paralelos sin tener que cambiar globalmente el contexto de la sesión con Set-AzContext.

2. Pasar Parámetros por Pipeline (ValueFromPipelineByPropertyName)
En la sección Object-Oriented Pipeline, describes cómo filtrar y ordenar. El examen AZ-104 evalúa si entiendes cómo PowerShell enlaza las propiedades de los objetos de manera implícita a través del pipeline para realizar acciones en lote (Bulk Operations):

Vinculación por Nombre: Cuando ejecutas un comando como Get-AzResourceGroup -Name "MyRG" | Get-AzVM, los cmdlets del módulo Az están programados para mapear automáticamente la propiedad .ResourceGroupName o .Name del objeto entrante al parámetro correspondiente del siguiente cmdlet. Esto permite apagar todas las máquinas virtuales de un grupo de recursos con una sola línea ultra-eficiente:

PowerShell
Get-AzVM -ResourceGroupName "Prod-RG" | Stop-AzVM -Force -NoWait
3. Operaciones de Larga Duración: El parámetro -NoWait y Jobs en PowerShell
Mencionas que se pueden automatizar implementaciones complejas. Para entornos de producción y preguntas de optimización de tiempos de ejecución en el examen, es mandatorio documentar cómo liberar la sesión de PowerShell ante despliegues pesados:

El flag -NoWait: Al igual que en la CLI, cmdlets como New-AzVM o Remove-AzResourceGroup incluyen el parámetro -NoWait. Esto instruye a la sesión a enviar la directiva a ARM y entregar el control de la consola inmediatamente con un estado Accepted.

El parámetro -AsJob: Transforma la ejecución del cmdlet en un PowerShell Background Job local. Esto permite al administrador monitorear el progreso del despliegue en segundo plano usando Get-Job, Receive-Job y Wait-Job, posibilitando la ejecución de otras tareas lógicas en el script principal mientras Azure procesa el hardware.
