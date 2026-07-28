## Bloodhound 
Luego de validar que las credenciales obtenidas eran funcionales dentro del dominio `raynex.lab`, inicié la fase de enumeración de Active Directory.

El objetivo de esta etapa fue obtener una representación completa de la estructura interna del dominio, identificando relaciones entre usuarios, grupos, equipos, sesiones activas y permisos delegados.

Mediante la información recolectada pude analizar las relaciones existentes entre objetos de Active Directory y detectar configuraciones inseguras que podían representar posibles rutas de escalada de privilegios.

## Preguntas Claves

- ¿Qué privilegios posee mi usuario comprometido?
- ¿Qué grupos pueden influenciar mi cuenta?
- ¿Existen permisos delegados incorrectamente?
- ¿Hay caminos indirectos que permitan alcanzar privilegios elevados?


## Ejecución 

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
