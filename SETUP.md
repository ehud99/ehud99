# Setup del perfil

Documento interno del repo. No se muestra en el perfil (GitHub solo renderiza `README.md`).

---

## 1. Desplegar tu propia instancia de github-readme-stats

**Por qué:** la instancia pública `github-readme-stats.vercel.app` no tiene acceso a tu cuenta, así que
**no puede ver tus repositorios privados**. Como la mayor parte de tu trabajo es privado, las tarjetas de
estadísticas y de lenguajes saldrían casi vacías y no reflejarían COBOL ni tu actividad real.
Con instancia propia + un token personal, sí las cuenta.

### Pasos

1. Haz un fork de <https://github.com/anuraghazra/github-readme-stats>.

2. Crea un **Personal Access Token** en <https://github.com/settings/tokens>
   (clásico) con los scopes:
   - `repo`      → acceso de lectura a tus repos privados
   - `read:user` → datos de tu perfil

   Copia el token. No lo pegues en ningún archivo de este repo.

3. Entra en <https://vercel.com>, inicia sesión con GitHub e importa tu fork.

4. Antes de desplegar, en **Environment Variables** añade:

   | Name    | Value        |
   |---------|--------------|
   | `PAT_1` | tu token     |

   (Si en el futuro topas con el rate limit, puedes añadir `PAT_2`, `PAT_3`… con tokens distintos.)

5. Despliega. Vercel te dará un dominio tipo `mi-github-stats.vercel.app`.

6. Sustituye en `README.md` y `README.en.md` todas las apariciones de
   `{{TU-INSTANCIA}}.vercel.app` por tu dominio real.

7. Verifica abriendo la URL en el navegador. Si las cifras siguen siendo solo las públicas,
   revisa que el token tenga el scope `repo` y que la variable se llame exactamente `PAT_1`.

> El parámetro `count_private=true` que ya viene en las URLs solo funciona en una instancia
> propia con PAT. En la instancia pública se ignora en silencio.

---

## 2. Widgets de terceros: riesgo conocido

| Widget | Servicio | Estado |
|---|---|---|
| Stats + Top Languages | tu instancia de Vercel | fiable, bajo tu control |
| Racha de contribuciones | `streak-stats.demolab.com` | demo compartida, con cortes y rate limit documentados |
| Gráfico de actividad | `github-readme-activity-graph.vercel.app` | el más frágil: ya cambió de host dos veces (Heroku y Cyclic cerraron) y tuvo caídas en septiembre de 2026 |

Si alguno deja de cargar y sale el recuadro roto, tienes dos salidas:

- **Autoalojarlo** también, igual que el punto 1 (ambos proyectos traen instrucciones de deploy).
- **Quitarlo** del README. Un perfil minimal-pro no pierde nada sin el gráfico de actividad.

Nota sobre imágenes en caché: GitHub sirve las imágenes externas a través de su proxy
`camo.githubusercontent.com`, que cachea también los fallos. Si arreglas un widget y sigue
viéndose roto, añadir un parámetro cualquiera a la URL (`&v=2`) fuerza a camo a tratarla como nueva.

---

## 3. Marcadores pendientes de rellenar

Todo lo que está entre `{{ }}` es un hueco. Para listarlos:

```bash
grep -n "{{" README.md README.en.md
```

Checklist:

- [ ] Apellido en el título (o quitarlo y dejar solo "Ehud")
- [ ] Ciudad, país, zona horaria y modalidad (remoto / híbrido / presencial)
- [ ] Nivel de inglés
- [ ] Años de experiencia en mainframe
- [ ] Tabla de stack: **borrar lo que no uses de verdad**, no dejarlo por rellenar
- [ ] Los 2–3 proyectos privados, con escala real
- [ ] Certificaciones y enlace a Credly
- [ ] LinkedIn, email de contacto, CV
- [ ] Dominio de tu instancia de Vercel
- [ ] Fun fact del cierre (o borrar esa línea)

> Sobre las métricas de escala: pon solo números que puedas defender en una entrevista.
> "Cartera de varios millones de cuentas" es mejor que una cifra inventada.

---

## 4. Antes de publicar

```bash
grep -c "{{" README.md README.en.md   # debe dar 0 y 0
git add -A && git commit -m "..." && git push
```

El repo `ehud99/ehud99` ya está enlazado como `origin`. Para poder hacer push desde la terminal:

```bash
gh auth login
```
