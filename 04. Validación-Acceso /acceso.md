## Validación del Acceso Privilegiado

Después de abusar de la relación ACL identificada, obtuve control sobre la cuenta privilegiada `raynex.lab\Administrador`.

Antes de continuar con las siguientes fases de la evaluación, realicé una validación de las credenciales obtenidas para confirmar que la escalada de privilegios había sido exitosa y que la nueva identidad podía autenticarse correctamente dentro del dominio.

Esta etapa es fundamental dentro de un escenario Red Team, ya que permite comprobar que el impacto identificado no es únicamente teórico, sino que representa un compromiso real de una cuenta con privilegios elevados.

Para validar el acceso utilicé **NetExec**, comprobando la autenticación SMB contra el Controlador de Dominio.

```bash
netexec smb 10.0.0.28 -u 'Administrador' -p 'Raynex2026' -d 'raynex.lab'
```

## Resultado 

```
SMB         10.0.0.28   445    DC01    [*] Windows Server 2022
SMB         10.0.0.28   445    DC01    [+] raynex.lab\Administrador:Raynex2026
```

La respuesta positiva del servicio confirmó que la cuenta Administrador era válida y que la escalada de privilegios mediante abuso de ACL había sido exitosa, lo que demuestra que la cadena completa del compromiso quedó validada.
