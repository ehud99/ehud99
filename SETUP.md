# Setup del perfil

Documento interno del repo. No aparece en el perfil: GitHub solo renderiza `README.md`.

---

## 1. Mostrar tus contribuciones privadas ← lo más importante

**Estado: pendiente. Es un checkbox y es lo que más cambia tu perfil.**

<https://github.com/settings/profile> → **"Include private contributions on my profile"**

### Por qué

Tu perfil te muestra a ti 1.280 contribuciones en el último año. Un visitante anónimo
ve algo completamente distinto. Descargando el calendario público sin sesión iniciada:

```
nivel 0 (días vacíos): 363 días
nivel 1:                 2 días
nivel 2:                 2 días
nivel 3:                 1 día
nivel 4:                 2 días
```

Siete días con actividad en todo el año. Por eso la tarjeta de racha mostraba
**10 Total Contributions**: no está fallando, está leyendo lo único que es público.
Todo tu trabajo real está en repositorios privados y GitHub no lo expone por defecto.

### Qué expone exactamente

Solo los **recuentos** del calendario, como contribuciones anónimas. No publica nombres
de repositorios, mensajes de commit, código ni organizaciones. Un visitante ve "hizo N
contribuciones este día" sin poder saber dónde.

Sin este ajuste, cualquier widget de actividad que pongas va a mentir a la baja, y un
reclutador que abra tu perfil verá un calendario casi vacío.

---

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
