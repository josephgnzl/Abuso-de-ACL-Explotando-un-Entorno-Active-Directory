## Acceso Inicial

Esta fase representó el punto inicial del compromiso dentro del entorno Active Directory.

 Ofensivamente contaba con credenciales válidas pertenecientes a un usuario del dominio, permitiendome la autenticación legítima contra los servicios internos.

A diferencia de un compromiso externo basado en explotación directa de servicios, este escenario muestra perfectamente una situación común en entornos empresariales: el atacante obtiene acceso utilizando una identidad legítima y posteriormente analiza las relaciones y permisos existentes dentro del dominio.

## Validación de Credenciales

Antes de iniciar la enumeración del entorno, validé que las credenciales obtenidas sean funcionales contra los servicios de Active Directory.

```bash
netexec smb 10.0.0.28 -u 'adiaz' -p 'Raynex2026' -d 'raynex.lab'
```

## Resultado
[+] raynex.lab\adiaz:Raynex2026 STATUS_LOGON_SUCCESS
