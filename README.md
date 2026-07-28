## Abuso de ACL: Explotando un Entorno Active Directory
Este repositorio nace a partir de una técnica de escalada de privilegios que encontré durante una evaluación de seguridad autorizada y que posteriormente recreé en mi laboratorio para comprenderla, documentarla y compartirla.

El objetivo es demostrar cómo un simple error en la delegación de permisos puede convertirse en una ruta directa hacia el compromiso de un entorno corporativo, así como entender el impacto, las técnicas de explotación y las medidas de mitigación.

## Cadena de Ataque

```text
Credenciales válidas
        |
        v
Usuario estándar (adiaz)
        |
        v
Enumeración con BloodHound
        |
        v
Identificación de GenericWrite sobre Administrator
        |
        v
Abuso de permisos ACL
        |
        v
Compromiso de cuenta privilegiada
```
## ¿Qué es ACL?
Una ACL (Access Control List o Lista de Control de Acceso) en Active Directory es una lista de permisos de seguridad asociada a un objeto como un usuario, grupo, equipo o unidad organizativa que define qué usuarios o grupos pueden acceder a él y qué acciones pueden realizar (escribir, borrar o cambiar contraseñas).
