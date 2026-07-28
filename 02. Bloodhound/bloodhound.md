## Bloodhound 
Luego de obtener credenciales válidas dentro del dominio `raynex.lab`, inicié la fase de enumeración de Active Directory.
El objetivo de esta etapa era obtener una representación del entorno interno del dominio, identificando relaciones entre usuarios, grupos, equipos y permisos asignados.
La información recolectada me permitió descubrir rutas de escalada de privilegios mediante configuraciones inseguras dentro del entorno corporativo.

## Representación 

```
bloodhound-python -c All -u adiaz -p 'Raynex2026' -d 'raynex.lab' -ns '10.0.0.28'

```

## Resultado 

La herramienta generó archivos JSON con información del dominio:

```
domains.json
users.json
groups.json
computers.json
sessions.json
acls.json
```
Estos archivos contienen información necesaria para construir el grafo de relaciones de Active Directory.

## Hallazgo
```
Usuario comprometido
        |
        v
Permiso ACL excesivo
        |
        v
Control sobre cuenta objetivo
        |
        v
Escalada de privilegios

```

Esta configuración me permitió construir una ruta de ataque hacia la cuenta Administrador con mayores privilegios dentro del dominio.
