# Setup del perfil

Documento interno del repo. No aparece en el perfil: GitHub solo renderiza `README.md`.

---

## 1. Activar las tarjetas de estadísticas

En `README.md` y `README.en.md`, la sección **Actividad** tiene dos tarjetas
(estadísticas y lenguajes más usados) **comentadas a propósito**.

**Por qué están desactivadas:** la instancia pública `github-readme-stats.vercel.app`
no tiene acceso a tu cuenta y **no puede ver repositorios privados**. Como los siete
repos de tu trabajo son privados, las tarjetas mostrarían cifras casi en cero y
lenguajes que no representan lo que haces. Vacías dicen algo peor que no estar.

La racha y el gráfico de actividad sí están activos: esos leen el calendario de
contribuciones, que **sí incluye tu actividad privada** si activas el ajuste del punto 2.

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

6. En ambos README:
   - Reemplaza `TU-INSTANCIA` por tu dominio.
   - Borra la línea `<!--` de apertura y la línea `-->` de cierre del bloque.

7. Comprueba abriendo la URL en el navegador. Si siguen saliendo solo cifras públicas,
   revisa que el token tenga scope `repo` y que la variable se llame exactamente `PAT_1`.

> El parámetro `count_private=true` que ya está puesto solo funciona en instancia propia
> con PAT. En la pública se ignora en silencio.

---

## 2. Mostrar contribuciones privadas

En <https://github.com/settings/profile> activa
**"Include private contributions on my profile"**.

Sin eso, tu gráfico de contribuciones y la racha salen casi vacíos aunque commitees a
diario, porque todo tu trabajo está en repos privados. Es el ajuste que más cambia
cómo se ve el perfil, y es gratis.

---

## 3. Widgets de terceros: riesgo conocido

| Widget | Servicio | Estado |
|---|---|---|
| Stats y lenguajes | tu instancia de Vercel | fiable, bajo tu control |
| Racha de contribuciones | `streak-stats.demolab.com` | demo compartida, con cortes y rate limit documentados |
| Gráfico de actividad | `github-readme-activity-graph.vercel.app` | el más frágil: cambió de host dos veces (Heroku y Cyclic cerraron) y tuvo caídas en septiembre de 2026 |

Si alguno deja de cargar y queda el recuadro roto: autoalojarlo igual que el punto 1,
o quitarlo del README. Un perfil sobrio no pierde nada sin el gráfico de actividad.

GitHub sirve las imágenes externas por su proxy `camo.githubusercontent.com`, que cachea
también los fallos. Si arreglas un widget y sigue viéndose roto, añadir un parámetro
cualquiera a la URL (`&v=2`) fuerza a camo a tratarla como nueva.

---

## 4. CV

`CV - Ehud Aguirre B.pdf` está en la carpeta pero **excluido por `.gitignore`**, porque
contiene tu número de teléfono y este repositorio es público. Un archivo commiteado aquí
queda accesible y permanece en el historial de git aunque después se borre.

Los README dicen "CV disponible a solicitud". Si prefieres enlazarlo, las opciones sanas son:

- Subirlo a Google Drive o Dropbox con enlace de solo lectura y poner esa URL.
- Generar una versión sin teléfono ni dirección, quitar `*.pdf` del `.gitignore` y
  commitear solo esa.
- Dejarlo como está: LinkedIn ya cubre esa función para un reclutador.

---

## 5. Publicar

```bash
gh auth login          # una sola vez
git push               # el remoto origin ya apunta a ehud99/ehud99
```

Después de publicar, revisa <https://github.com/ehud99> y comprueba que las imágenes
de la sección Actividad cargan bien.
