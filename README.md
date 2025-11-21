Documentación: Script de Carga Automática de Procesos por Cadena
1. Descripción General
>Script automatizado que genera cargas de datos para diferentes tipos de procesos (Sell Out, Pedidos, Comparativo, etc.) Basándose en la configuración de usuarios activos en la tabla de Credenciales. El script se ejecuta diariamente y determina qué procesos ejecutar según el día de la semana y la configuración del usuario.
>
2. Propósito
>Automatizar la generación de cargas de datos para múltiples cadenas retail
Gestionar diferentes tipos de movimientos (Sell Out, Pedidos, Comparativo, Forecast, Devoluciones, Compras, RecShip)
Diferenciar entre procesos diarios (Sell Out) y semanales (resto de procesos)
Registrar todas las operaciones en bitácora para trazabilidad
3. Usuario
>Debe cumplir todas estas condiciones:
Activo == 1 - Usuario activo en la tabla Credencial
Campo adicionales no nulo
Campo adicionales contiene al menos un proceso válido>
3.1 Día de la semana
>Sell Out: Se ejecuta todos los días
Otros procesos: Sólo se ejecutan los lunes
4. Configuración de Datos
>
4.1 Rango de fechas
| Fechaini | Fechafin |
|---------:|-----------|
|1 día |  7 días|
| Ayer| Hace 7 dias    |
5. Formas Involucradas
5.1 Credencial (Lectura)
```
Campos utilizados:
Cadena_Credencial - Nombre de la cadena retail
Usuario - Identificador del usuario
Activo - Estado del usuario (1 = activo)
Proveedor - Nombre del proveedor
adicionales - Procesos habilitados (separados por comas)
```

6. Troubleshooting
```
Problema: No se generan cargas
Verificar:Ambiente es producción
Usuario tiene Activo = 1
Campo adicionales no es null
Si no es Sell Out, verificar que sea lunes
Revisar logs para ver qué usuarios se procesaron
Problema: Algunas cadenas no procesan
Verificar:
Existe en tabla Tienda
Usuario tiene la cadena correcta en Cadena_Credencial
Revisar logs de "Procesando usuario"
```
