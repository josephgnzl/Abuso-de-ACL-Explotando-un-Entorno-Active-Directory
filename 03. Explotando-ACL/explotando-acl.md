## Explotación del Permiso ACL

Después de analizar las relaciones obtenidas mediante BloodHound, identifiqué el camino que conectaba la cuenta comprometida `raynex.lab\adiaz` con la cuenta privilegiada `raynex.lab\Administrator`.

El análisis reveló que el usuario `adiaz` contaba con el permiso ACL:

```text
GenericWrite
```
sobre el objeto correspondiente a la cuenta Administrator.

Este hallazgo representaba una debilidad significativa dentro de la configuración de Active Directory, ya que una cuenta con privilegios iniciales limitados tenía la capacidad de modificar propiedades del objeto objetivo.

Este tipo de delegaciones incorrectas pueden convertirse en una ruta directa de escalada de privilegios. El atacante no necesita explotar una vulnerabilidad del sistema operativo; simplemente abusa de permisos legítimos que fueron asignados de manera incorrecta.

## Abuso de la Relación ACL

Con el permiso identificado, procedí a validar el impacto real de la configuración encontrada.

La relación de confianza existente era:

```
raynex.lab\adiaz
        |
        |
        v
GenericWrite
        |
        |
        v
raynex.lab\Administrator
```
Esta relación permitió realizar modificaciones sobre la cuenta privilegiada y avanzar desde un usuario estándar comprometido hacia una identidad con mayores privilegios dentro del dominio.

## Ejecución del Ataque

Para realizar la modificación utilicé net rpc, una herramienta disponible en Kali Linux que permite interactuar con servicios RPC de Windows.

El objetivo era enviar una solicitud al Controlador de Dominio para modificar la contraseña de la cuenta Administrator utilizando los permisos previamente identificados.

```
net rpc password Administrator "Raynex2026" -U "adiaz%Raynex2026" -S 10.0.0.28
```

## Resultado

La operación fue ejecutada correctamente, demostrando que la cuenta comprometida inicialmente podía afectar directamente una cuenta administrativa del dominio.

Una mala asignación de ACLs puede convertir una cuenta de bajo privilegio en un punto de entrada hacia el control administrativo del dominio.
