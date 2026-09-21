# Setup del perfil

Documento interno del repo. No aparece en el perfil: GitHub solo renderiza `README.md`.

---

## 1. Mostrar tus contribuciones privadas — HECHO

Ajuste activado en <https://github.com/settings/profile> →
**"Include private contributions on my profile"**.

Efecto medido sobre el calendario publico (consultado sin sesion iniciada):

| | antes | despues |
|---|---|---|
| Dias con actividad | 7 | 165 |
| Dias vacios | 363 | 206 |
| Total que reporta el widget | 10 | 1.282 |

Solo se exponen los **recuentos** del calendario, como contribuciones anonimas: no
publica nombres de repositorios, mensajes de commit, codigo ni organizaciones.

### Si la tarjeta sigue mostrando los numeros viejos

Es el proxy de imagenes de GitHub. `camo.githubusercontent.com` cachea las imagenes
externas, incluidas las respuestas antiguas, y no siempre refresca aunque el servicio
de origen ya devuelva datos nuevos. La URL de la racha en ambos README lleva `&v=2`
justo para forzar a camo a tratarla como una imagen nueva. Si vuelve a quedarse
pegada, sube el numero: `&v=3`, `&v=4`, y commitea.

## 2. Activar las tarjetas de estadísticas

En ambos README, la sección **Actividad** tiene dos tarjetas (estadísticas y lenguajes
más usados) **comentadas a propósito**.

**Por qué están desactivadas:** la instancia pública `github-readme-stats.vercel.app`
no tiene acceso a tu cuenta y no puede ver repositorios privados. Como los siete repos
de tu trabajo son privados, las tarjetas mostrarían cifras en cero y lenguajes que no
representan lo que haces.

> Ojo: el punto 1 **no** arregla esto. El ajuste de contribuciones privadas afecta al
> calendario, no a la API de repositorios. Para que estas dos tarjetas cuenten repos
> privados hace falta instancia propia con token. Son cosas independientes.

### Desplegar tu instancia

1. Fork de <https://github.com/anuraghazra/github-readme-stats>.

2. Crea un **Personal Access Token** en <https://github.com/settings/tokens> (classic)
   con los scopes:
   - `repo` → lectura de tus repos privados
   - `read:user` → datos de tu perfil

   No pegues el token en ningún archivo de este repositorio.

3. En <https://vercel.com>, inicia sesión con GitHub e importa tu fork.

4. Antes de desplegar, en **Environment Variables**:

   | Name    | Value    |
   |---------|----------|
   | `PAT_1` | tu token |

   Si más adelante topas con el rate limit, añade `PAT_2`, `PAT_3`… con tokens distintos.

5. Despliega. Vercel te da un dominio tipo `mi-stats.vercel.app`.

6. En `README.md` y `README.en.md`:
   - Reemplaza `TU-INSTANCIA` por tu dominio.
   - Borra la línea `<!--` de apertura y la línea `-->` de cierre del bloque.

7. Comprueba abriendo la URL en el navegador. Si siguen saliendo solo cifras públicas,
   revisa que el token tenga scope `repo` y que la variable se llame exactamente `PAT_1`.

> El parámetro `count_private=true` que ya está puesto solo funciona en instancia propia
> con PAT. En la pública se ignora en silencio.

---

## 3. Widgets de terceros

| Widget | Servicio | Estado |
|---|---|---|
| Stats y lenguajes | tu instancia de Vercel | fiable, bajo tu control (pendiente, punto 2) |
| Racha de contribuciones | `streak-stats.demolab.com` | activo, responde 200; demo compartida con cortes y rate limit documentados |
| ~~Gráfico de actividad~~ | `github-readme-activity-graph.vercel.app` | **eliminado del README** |

### Por qué se eliminó el gráfico de actividad

El servicio devuelve:

```
HTTP 402 — Payment required
DEPLOYMENT_DISABLED
```

El deployment de Vercel del mantenedor está deshabilitado por facturación, así que la
imagen sale rota para todo el mundo. No es una caída pasajera que se arregle esperando.
El proyecto ya había cambiado de host dos veces antes (Heroku y Cyclic cerraron).

Tampoco se pierde nada: GitHub ya dibuja tu calendario de contribuciones justo debajo
del README en la página del perfil, así que el widget duplicaba información. Si aun así
lo quieres, habría que autoalojarlo como en el punto 2.

### Imágenes que siguen viéndose rotas

GitHub sirve las imágenes externas por su proxy `camo.githubusercontent.com`, que cachea
también los fallos. Si un widget se arregla y sigue saliendo roto, añadir un parámetro
cualquiera a la URL (`&v=2`) fuerza a camo a tratarla como nueva.

---

## 4. CV

`CV - Ehud Aguirre B.pdf` está en la carpeta pero **excluido por `.gitignore`**, porque
contiene tu número de teléfono y este repositorio es público. Un archivo commiteado aquí
queda accesible y permanece en el historial de git aunque después se borre.

Los README dicen "CV disponible a solicitud". Si prefieres enlazarlo:

- Subirlo a Google Drive o Dropbox con enlace de solo lectura y poner esa URL.
- Generar una versión sin teléfono ni dirección, quitar `*.pdf` del `.gitignore` y
  commitear solo esa.
- Dejarlo como está: LinkedIn ya cubre esa función para un reclutador.

---

## 5. Publicar

```bash
git push               # el remoto origin ya apunta a ehud99/ehud99
```

Después de publicar, abre <https://github.com/ehud99> **en una ventana de incógnito**.
Es la única forma de ver el perfil como lo ve un reclutador: con tu sesión iniciada
GitHub te enseña datos privados que los demás no ven.
