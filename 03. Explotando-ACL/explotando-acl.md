## Explotando ACL

Una vez identificado el borde `GenericWrite` desde `adiaz` hacia `Administrator` (o `ADMINISTRADOR`), se procede a abusar de este permiso para tomar el control del dominio.

### ¿Qué significa `GenericWrite`?

Este permiso otorga a `adiaz` la capacidad de modificar **cualquier atributo** del objeto `Administrator`, incluyendo:

- `unicodePwd` → Contraseña del usuario.
- `member` → Pertenencia a grupos (si se aplica sobre un grupo).
- `sAMAccountName` → Nombre de la cuenta.
- `servicePrincipalName` → SPNs (para Kerberoasting).

**En este caso, abusamos de la capacidad de restablecer la contraseña sin conocer la actual.**

### Comando utilizado

Para abusar del permiso identificado se utilizó `net rpc`, aprovechando la capacidad de modificar la contraseña del usuario objetivo mediante los servicios RPC de Windows (protocolo SAMR sobre SMB).

```bash
net rpc password ADMINISTRADOR "Raynex2026" -U "adiaz%Raynex2026" -S 192.168.0.110
```
