## Validación Acceso 

Después de abusar de la relación ACL identificada, se obtuvo control sobre la cuenta objetivo dentro del dominio.

En esta fase validé que las credenciales obtenidas fueran funcionales y que la cuenta comprometida pueda autenticarse correctamente contra los servicios de Active Directory.
El objetivo es confirmar que la escalada fue exitosa antes de continuar con la fase de acceso remoto.

Se utilizó NetExec para validar que las credenciales fueran aceptadas por el dominio.

```bash
netexec smb 10.0.0.28 -u 'Administrador' -p 'Raynex2026' -d 'raynex.lab'
```

## Resultado
```
SMB         10.0.0.28   445    DC01    [*] Windows Server 2022
SMB         10.0.0.28   445    DC01    [+] raynex.lab\Administrador:Raynex2026
```
