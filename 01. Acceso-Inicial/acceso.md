## Acceso Inicial

Esta fase representó el punto inicial del compromiso dentro del entorno Active Directory.

Durante esta etapa contaba con credenciales válidas pertenecientes a un usuario del dominio, lo que me permitió realizar una autenticación legítima contra los servicios internos del entorno.

A diferencia de un compromiso externo basado en la explotación directa de servicios expuestos, este escenario representa una situación común dentro de ambientes empresariales: un atacante logra obtener acceso utilizando una identidad válida y posteriormente comienza a analizar la estructura del dominio, las relaciones entre objetos y los permisos asignados con el objetivo de identificar posibles rutas de escalada de privilegios.


## Validación de Credenciales

Antes de iniciar cualquier proceso de enumeración, validé que las credenciales obtenidas fueran funcionales contra los servicios de Active Directory.

Para esta validación utilicé **NetExec**, comprobando la autenticación SMB contra el controlador de dominio.

```bash
netexec smb 10.0.0.28 -u 'adiaz' -p 'Raynex2026' -d 'raynex.lab'
## Resultado
[+] raynex.lab\adiaz:Raynex2026 STATUS_LOGON_SUCCESS
