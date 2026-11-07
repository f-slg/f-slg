<h1 align="center">Dr. Fabricio Salas Guerrero</h1>

<p align="center"><strong>Médico epidemiólogo · Salud digital · Interoperabilidad clínica · Ingeniería de datos</strong></p>

<p align="center"><strong>Español</strong> · <a href="https://github.com/f-slg/f-slg/blob/main/README.en.md">English</a></p>

<p align="center">
  <a href="https://www.hl7ecuador.org/">HL7 Ecuador</a> ·
  <a href="https://www.linkedin.com/in/fslg/">LinkedIn</a> ·
  <a href="https://aipocrates.blog/">AIpócrates</a> ·
  <a href="https://github.com/f-slg?tab=repositories">Repositorios</a>
</p>

---

### De datos clínicos interoperables a inteligencia territorial

Desarrollo herramientas abiertas que conectan **estándares clínicos, bases de datos, analítica y cartografía**, para convertir información dispersa en datos reutilizables para investigación, vigilancia epidemiológica y decisiones en salud pública.

Presido **[HL7 Ecuador](https://www.hl7ecuador.org/)**. Trabajo con **R, HL7 FHIR R4, SQL on FHIR, DuckDB, `sf` y Shiny**, y publico materiales para aprender y reproducir resultados.

<p align="center">
  <a href="#paquetes-de-r">Paquetes</a> ·
  <a href="#cómo-se-relacionan">Arquitectura</a> ·
  <a href="#aprendizaje-y-prototipos">Aprendizaje</a> ·
  <a href="#investigación-y-trayectoria">Investigación</a> ·
  <a href="#colaboración">Contacto</a>
</p>

## Paquetes de R

| Paquete | Para qué sirve | Estado |
|---|---|---|
| [**fhirviews**](https://github.com/f-slg/fhirviews) | Cliente HL7 FHIR R4 y motor SQL on FHIR (`ViewDefinition`) que convierte recursos clínicos en tablas. | [![R-CMD-check](https://github.com/f-slg/fhirviews/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/f-slg/fhirviews/actions/workflows/R-CMD-check.yaml) [![SQL on FHIR](https://img.shields.io/badge/SQL%20on%20FHIR-133%2F133%20shareable-0F6B82)](https://f-slg.github.io/fhirviews/reference/vista_conformidad.html) |
| [**geoecu**](https://github.com/f-slg/geoecu) | Provincias, cantones y parroquias del Ecuador como objetos `sf`, con códigos DPA del CONALI. | [![CRAN](https://www.r-pkg.org/badges/version/geoecu)](https://cran.r-project.org/package=geoecu) [![R-CMD-check](https://github.com/f-slg/geoecu/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/f-slg/geoecu/actions/workflows/R-CMD-check.yaml) |
| [**pobecu**](https://github.com/f-slg/pobecu) | Población del INEC por provincia, cantón y parroquia, lista para usar como denominador de tasas. | [![R-CMD-check](https://github.com/f-slg/pobecu/actions/workflows/R-CMD-check.yaml/badge.svg)](https://github.com/f-slg/pobecu/actions/workflows/R-CMD-check.yaml) |

<sub>Cada paquete tiene su README en español y en inglés. Las funciones y la documentación de referencia están en español.</sub>

### fhirviews — HL7 FHIR → tablas analíticas

[Documentación](https://f-slg.github.io/fhirviews/) · [Arquitectura](https://f-slg.github.io/fhirviews/articles/arquitectura.html) · [Conformidad](https://f-slg.github.io/fhirviews/reference/vista_conformidad.html)

Consulta servidores **FHIR R4** desde R y RStudio (búsqueda con paginación, CRUD, transacciones, `$everything`, `$export`, SMART on FHIR) y transforma los recursos en `data.frame` con **ViewDefinition** y **FHIRPath**. Incluye un motor experimental sobre **DuckDB** para millones de recursos en NDJSON o Parquet. Supera las 133 pruebas *shareable* de la suite oficial de SQL on FHIR. Es un resultado de pruebas de implementación, no una certificación externa.

```mermaid
flowchart LR
    F["Recursos FHIR R4"] --> E["fhirviews<br/>motor SQL on FHIR"]
    V["ViewDefinition<br/>FHIRPath"] --> E
    E --> T["data.frame"] --> D["DuckDB · ggplot2 · Shiny"]
```

### geoecu — cartografía oficial como objetos sf

[Documentación](https://f-slg.github.io/geoecu/) · [Galería cartográfica](https://f-slg.github.io/geoecu/articles/galeria.html)

**24 provincias, 223 cantones y 1.048 parroquias** que encajan sin huecos ni traslapes, en dos resoluciones, con superficie `area_km2`, unión por código DPA (`geoecu_unir()`), conversión de códigos históricos (`actualizar_codigo()`) y caché verificada para trabajar sin conexión.

<table>
  <tr>
    <td width="33%"><a href="https://github.com/f-slg/geoecu#1-provincias-regiones-naturales-y-límites"><img src="https://raw.githubusercontent.com/f-slg/geoecu/main/man/figures/README-provincias.png" width="100%" alt="Mapa de las 24 provincias del Ecuador coloreadas por región natural, con Galápagos en recuadro" /></a></td>
    <td width="33%"><a href="https://github.com/f-slg/geoecu#2-cantones-parroquias-por-cantón"><img src="https://raw.githubusercontent.com/f-slg/geoecu/main/man/figures/README-cantones.png" width="100%" alt="Mapa de los cantones del Ecuador coloreados por número de parroquias" /></a></td>
    <td width="34%"><a href="https://github.com/f-slg/geoecu#3-parroquias-mapa-nacional-y-detalle-de-puyango"><img src="https://raw.githubusercontent.com/f-slg/geoecu/main/man/figures/README-parroquias.png" width="100%" alt="Mapa parroquial del Ecuador según tipo de parroquia, con detalle de Puyango, Loja" /></a></td>
  </tr>
  <tr>
    <td align="center"><sub>Provincias · regiones naturales</sub></td>
    <td align="center"><sub>Cantones · parroquias por cantón</sub></td>
    <td align="center"><sub>Parroquias · detalle de Puyango</sub></td>
  </tr>
</table>

<sub>Fuente: CONALI, División Político-Administrativa (datos abiertos, CC BY). Galápagos se reubica solo para visualización.</sub>

### pobecu — denominadores para indicadores de salud

[Documentación](https://f-slg.github.io/pobecu/) · [Metodología](https://f-slg.github.io/pobecu/articles/metodologia.html) · [Mapas con geoecu](https://f-slg.github.io/pobecu/articles/pobecu-geoecu.html)

Estimaciones y proyecciones oficiales del **INEC (Revisión 2024)**: nacional 1950–2050, provincial 1990–2035 y cantonal 2010–2035 por sexo, edad y área urbana/rural, más una **estimación parroquial propia** 2010–2035 coherente con el total cantonal. Calcula tasas en una línea con `pob_tasa()` y homologa códigos CONALI con los del Censo 2022. Se auditaron **más de seis millones de celdas** contra los Excel del INEC, sin diferencias ([validación](https://github.com/f-slg/pobecu/tree/main/validacion)).

<a href="https://github.com/f-slg/pobecu">
  <img src="https://raw.githubusercontent.com/f-slg/pobecu/main/man/figures/README-principal.png" width="100%" alt="Tres paneles: población del Ecuador 1950-2050, pirámides de 2025 y 2050, y densidad de población de los 221 cantones en 2025">
</a>

<sub>Fuente: INEC, Revisión 2024. Las cifras parroquiales son estimaciones de pobecu, no cifras oficiales.</sub>

## Cómo se relacionan

**Datos clínicos interoperables + denominadores poblacionales + geografía administrativa.** Los paquetes son independientes, pero están pensados para usarse juntos:

```mermaid
flowchart LR
    F["Fuentes HL7 FHIR R4"] --> V["fhirviews<br/>FHIR → tablas"]
    V --> A["Casos"]
    P["pobecu<br/>Población INEC"] --> I["Tasas e indicadores"]
    A --> I
    I --> G["geoecu<br/>Mapas DPA"]
```

Del registro de casos a un mapa de tasas:

```r
library(pobecu)   # denominadores del INEC
library(ggplot2)

casos <- data.frame(dpa_canton = c("1101", "1102", "1110"), anio = 2025,
                    casos = c(120, 8, 15))          # datos ficticios
tasas <- pob_tasa(casos, "casos", por = 1e5)        # casos por 100 000 hab.

mapa <- pob_mapa("canton", anio = 2025, provincia = "Loja")   # capa de geoecu
mapa <- merge(mapa, tasas[c("dpa_canton", "tasa")], by = "dpa_canton", all.x = TRUE)

ggplot(mapa) + geom_sf(aes(fill = tasa)) + theme_void()
```

<a href="https://github.com/f-slg/geoecu#6-densidad-poblacional-provincias-cantones-y-parroquias">
  <img src="https://raw.githubusercontent.com/f-slg/geoecu/main/man/figures/README-densidad.png" width="100%" alt="Tres mapas del Ecuador con la densidad poblacional en habitantes por km² por provincia, cantón y parroquia, con escala logarítmica común">
</a>

<sub>Densidad poblacional 2026: población del INEC (vía pobecu) / `area_km2` de geoecu.</sub>

## Aprendizaje y prototipos

| Proyecto | Para qué sirve |
|---|---|
| [**Aprende FHIR**](https://github.com/f-slg/aprende-fhir) · [sitio](https://f-slg.github.io/aprende-fhir/) | Taller de HL7 FHIR R4 en español, paso a paso, con fichas por recurso y un caso clínico ecuatoriano, para Postman, R o curl. |
| [**Agenda FHIR**](https://github.com/f-slg/agenda-fhir-r) | Prototipo educativo de agenda clínica en R/Shiny con recursos FHIR y datos sintéticos. |
| [**sql-on-fhir.js**](https://github.com/f-slg/sql-on-fhir.js) | Mi *fork* de la implementación de referencia de SQL on FHIR, para contribuir el informe de conformidad de fhirviews. |

Los ejemplos públicos usan información sintética o de fuentes abiertas. Los prototipos son educativos y no sustituyen la validación institucional ni la certificación clínica.

## Investigación y trayectoria

- **HL7 Ecuador:** presidencia y promoción de estándares de interoperabilidad. [Capítulo HL7 Ecuador](https://www.hl7ecuador.org/) · [Actividad institucional](https://www.linkedin.com/company/hl7-ecuador/).
- **Universidad Nacional de Loja:** [comité científico Cienf 2026](https://unl.edu.ec/cienf2026/comite-cientifico).
- Villagrán Pancho LE, **Salas Guerrero RF**, et al. *Metodología en la optimización de bases de datos de los sistemas de información en salud de Ecuador para el monitoreo en tiempo real de eventos críticos para la vigilancia epidemiológica*. **Práctica Familiar Rural** (2023). [DOI: 10.16921/pfr.v8i3.292](https://doi.org/10.16921/pfr.v8i3.292).
- Pérez-Tasigchana F, et al. (incluye a **Ronald Salas**). *Effectiveness of COVID-19 vaccines in Ecuador: A test-negative design*. **Vaccine: X** 15 (2023), 100404. [DOI: 10.1016/j.jvacx.2023.100404](https://doi.org/10.1016/j.jvacx.2023.100404) · [PubMed](https://pubmed.ncbi.nlm.nih.gov/38033879/).

<details>
<summary><strong>Formación</strong></summary>

- Medicina y maestría en Epidemiología, Universidad Nacional de Loja.
- **DBA en curso**, Walsh College, orientado a aplicaciones de IA y *machine learning*.
- Formación en gerencia de instituciones de salud, telemedicina, interoperabilidad y ciencia de datos.
- Educación ejecutiva en IA/ML con UT Austin McCombs / Great Learning.
- Estándares FHIR y terminologías como SNOMED CT.

Historial académico, cargos y certificaciones actualizados en [LinkedIn](https://www.linkedin.com/in/fslg/).

</details>

<details>
<summary><strong>Divulgación</strong></summary>

- [La interoperabilidad basada en inteligencia artificial: ¿la nueva torre de Babel?](https://aipocrates.blog/2025/03/09/la-interoperabilidad-basada-en-inteligencia-artificial-la-nueva-torre-de-babel/)
- [El médico, la IA y la autopista cuántica (Parte 1)](https://aipocrates.blog/2025/08/03/el-medico-la-ia-y-la-autopista-cuantica-repensando-el-futuro-de-la-medicina-desde-la-interoperabilidad-sistemica-parte-1-2/)
- [AIpócrates](https://aipocrates.blog/): reflexiones sobre IA, estándares y transformación de la salud.

</details>

## Colaboración

Me interesan colaboraciones que combinen **FHIR, SQL on FHIR, R, datos públicos reproducibles e inteligencia territorial en salud**, especialmente en Latinoamérica.

Propuestas académicas o institucionales: [LinkedIn](https://www.linkedin.com/in/fslg/). Errores o contribuciones de código: *Issues* y *Pull Requests* de cada repositorio, en español o en inglés.

<p align="center"><sub>Proyectos abiertos · Fuentes identificadas · Datos sintéticos en demostraciones · Documentación reproducible</sub></p>
