## Acceso Remoto y Mitigación

Después de confirmar la escalada de privilegios y validar que la cuenta `raynex.lab\Administrador` podía autenticarse correctamente dentro del dominio, procedí a establecer una sesión remota contra el Controlador de Dominio.

El objetivo de esta fase fue demostrar el impacto final de la ruta de ataque identificada: pasar de un usuario con privilegios limitados a una identidad administrativa con capacidad de ejecutar comandos remotamente dentro del entorno Active Directory.

En un escenario real de Red Team, obtener una cuenta privilegiada no representa únicamente acceso a un usuario, sino la posibilidad de interactuar con sistemas críticos, realizar movimiento lateral y comprometer otros recursos del dominio.

---
## Establecimiento de Sesión Remota

Para la conexión remota utilicé **Evil-WinRM**, una herramienta basada en PowerShell Remoting que permite interactuar con sistemas Windows mediante el servicio **Windows Remote Management (WinRM)**.

La autenticación se realizó utilizando las credenciales obtenidas después del abuso de la relación ACL.

Comando utilizado:

```bash
evil-winrm -i '10.0.0.28' -u 'Administrador' -p 'Raynex2026'
```

## Resultado 

La sesión remota fue establecida correctamente:

```
*Evil-WinRM* PS C:\Users\Administrador\Documents>
```

Este resultado confirmó que el compromiso fue exitoso y que la cuenta obtenida mediante el abuso de ACL tenía la capacidad de ejecutar comandos dentro del sistema objetivo.

## Mitigación

Para prevenir este tipo de escaladas de privilegios mediante abuso de ACLs, sugiero:

- Revisar periódicamente las delegaciones de permisos dentro del dominio para identificar asignaciones innecesarias o configuraciones incorrectas.
- Aplicar estrictamente el principio de mínimo privilegio, garantizando que usuarios, grupos y objetos únicamente posean los permisos necesarios para cumplir sus funciones.
- Eliminar permisos excesivos sobre cuentas privilegiadas y objetos críticos del dominio.
- 
- Auditar especialmente la presencia de permisos sensibles como:
  - `GenericAll`
  - `GenericWrite`
  - `WriteDACL`
  - `WriteOwner`
  - `ForceChangePassword`

Hack the Planet 

- Joseph 
