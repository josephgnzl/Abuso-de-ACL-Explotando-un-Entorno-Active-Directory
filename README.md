## Abuso de ACL: Explotando un Entorno Active Directory
Este repositorio documenta una técnica de escalada de privilegios que identifiqué durante una evaluación de seguridad autorizada y que posteriormente llevé a mi laboratorio para estudiarla, explotarla y dominar cada detalle de su funcionamiento.

El objetivo es demostrar cómo un simple error en la delegación de permisos puede convertirse en una ruta directa hacia el compromiso de un entorno corporativo, así como entender el impacto, las técnicas de explotación y las medidas de mitigación.

## Cadena de Ataque

```text
Credenciales Válidas
        |
        v
Usuario Estándar (adiaz)
        |
        v
Enumeración con BloodHound
        |
        v
Identificación de GenericWrite sobre usuario Administrador
        |
        v
Abuso de Permisos ACL
        |
        v
Compromiso de cuenta Administrador Privilegiada
```
## ¿Qué es ACL?
Una ACL (Access Control List o Lista de Control de Acceso) en Active Directory es una lista de permisos de seguridad asociada a un objeto como un usuario, grupo, equipo o unidad organizativa que define qué usuarios o grupos pueden acceder a él y qué acciones pueden realizar (escribir, borrar o cambiar contraseñas).
