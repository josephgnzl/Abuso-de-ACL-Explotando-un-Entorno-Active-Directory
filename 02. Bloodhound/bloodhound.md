## Bloodhound 
Luego de obtener credenciales válidas dentro del dominio `raynex.lab`, inicié la fase de enumeración de Active Directory.

El objetivo de esta etapa era obtener una representación del entorno interno del dominio, identificando relaciones entre usuarios, grupos, equipos y permisos asignados.

La información recolectada me permitió descubrir rutas de escalada de privilegios mediante configuraciones inseguras dentro del entorno corporativo.

## Representación 

```
bloodhound-python -c All -u adiaz -p 'Raynex2026' -d 'raynex.lab' -ns '10.0.0.28'

```
