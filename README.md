# Phoenix Clientes

CRM personal de **Phoenix IA Method** para el celular y cualquier PC. Es una sola página HTML, sin dependencias ni compilación, que corre como *artifact* de Claude y guarda los datos en la base de datos del artifact (`window.claude.use("db")`). Este repositorio tiene **solo el código**: ningún dato de clientes vive aquí.

## Qué hace

- **Hoy:** a quién le toca contacto hoy, quiénes están por retomar y quiénes no tienen próximo toque. Regla de la casa: ningún cliente abierto sin próximo toque (fecha + qué le aportas).
- **Clientes:** buscador y filtros por estado (abiertos, ganados, en pausa, perdidos).
- **Embudo:** clientes por etapa de venta, con el monto en juego, y dónde se traba el cambio según ADKAR.
- **Ficha del cliente:** llamar, WhatsApp o correo con un toque; registrar contactos; pendientes; bitácora; datos del negocio y de la entrega.
- **Gestión del cambio (ADKAR), desde la versión 2:** cada cliente se mide de 1 a 5 en Conciencia, Deseo, Conocimiento, Habilidad y Refuerzo. La app calcula sola el **punto de barrera** (la primera etapa con 3 o menos), lo muestra en la tarjeta del cliente y sugiere qué hacer para subirlo.

## Modelo de datos

Colección `clientes` (un documento por cliente) con las subcolecciones `bitacora` (`fecha`, `texto`, `creado`) y `pendientes` (`texto`, `hecho`, `orden`).

| Grupo | Campos |
|---|---|
| Contacto | `nombre`, `empresa`, `telefono`, `email`, `canal`, `decisor`, `rubro`, `ciudad` |
| Venta | `etapa`, `resultado`, `proximoToque`, `proximoQue`, `proximaReunion`, `ultimoContacto`, `dolor`, `solucion`, `monto`, `mensualidad`, `moneda`, `venceEl` |
| Entrega | `entregaPlazo`, `entregaFecha`, `entregaNota` |
| ADKAR | `adkarA`, `adkarD`, `adkarK`, `adkarH` (la segunda A, habilidad), `adkarR` (1 a 5 o `null`), `adkarNota`, `adkarActualizado` |
| Registro | `notas`, `creado`, `actualizado` |

## Seguridad

- La base de datos solo la puede leer y escribir su dueño (regla `owner` en lectura y escritura).
- Todo texto que viene de la base se escapa antes de pintarse en la página.
- No hay claves, tokens ni datos personales en el código.

## Stack

HTML, CSS y JavaScript sin librerías. Tipografías Caladea y Carlito (Google Fonts). Modo claro y oscuro.
