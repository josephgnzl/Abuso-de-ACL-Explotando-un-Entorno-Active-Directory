## Explotando ACL

Una vez que BloodHound me mostró el camino, confirmé que el usuario `adiaz` tenía el permiso `GenericWrite` sobre la cuenta del `Administrator`. Ese hallazgo fue el punto de inflexión.

Este permiso, en términos prácticos, le otorga a `adiaz` la capacidad de modificar atributos clave de la cuenta objetivo. Entre ellos, el más crítico es la contraseña. Active Directory permite restablecerla sin necesidad de conocer la actual, siempre que se cuente con el permiso adecuado. Esa fue la vía que aproveché.

Para ejecutar el ataque utilicé `net rpc`, una herramienta nativa de Kali Linux que se comunica con los servicios RPC de Windows. Con ella, se le ordena al Controlador de Dominio que cambiara la contraseña del Administrador por una que nosotros controlamos.

El comando que materializó el acceso fue el siguiente:

```bash
net rpc password ADMINISTRADOR "Raynex2026" -U "adiaz%Raynex2026" -S 10.0.0.28
```
