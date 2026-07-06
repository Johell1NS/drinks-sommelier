# drinks-sommelier

<p align="center">
  <img src="../img/drinks-sommelier-logo.png" alt="drinks-sommelier" width="600">
</p>

<p align="center"><a href="../README.md">English</a> · <a href="README.zh-CN.md">简体中文</a> · <b>Español</b> · <a href="README.ja.md">日本語</a> · <a href="README.ko.md">한국어</a> · <a href="README.pt-BR.md">Português (Brasil)</a> · <a href="README.fr.md">Français</a> · <a href="README.de.md">Deutsch</a> · <a href="README.ru.md">Русский</a> · <a href="README.ar.md">العربية</a> · <a href="README.hi.md">हिन्दी</a> · <a href="README.it.md">Italiano</a></p>

<p align="center">
  <strong>Un sommelier en tu bolsillo, siempre a tu lado.</strong><br>
  <em>Estantes, menús, bodegas: dondequiera que estés, sabe qué recomendarte.</em>
</p>

> **Una skill para agentes de IA.** OpenClaw, Hermes Agent, OpenCode, Claude Code, Cursor y más.
> Un sommelier virtual especializado en cervezas y vinos que aprende tus gustos
> personales y sugiere la mejor elección de cualquier estante, menú
> o lista. **Gratuito, de código abierto, autogestionado.**

---

## Por qué existe

En el restaurante, en el pub, en la tienda de vinos, en el supermercado: el problema es siempre
el mismo. **Docenas de opciones y ninguna certeza** sobre qué elegir que sea
verdaderamente adecuado a tus gustos.

Podrías preguntar al camarero, abrir cinco pestañas en tu móvil, o
esperar que el nombre más bonito sea también el mejor. O puedes preguntar
a tu agente de IA — y él ya sabe lo que te gusta.

**drinks-sommelier** enseña a cualquier agente de IA a actuar como un
sommelier personal. El agente:

1. Aprende tus preferencias de gusto, de una vez por todas
2. Analiza cualquier entrada: foto de un estante, menús digitales, listas
   de nombres escritas por el usuario
3. Busca información actualizada sobre cada producto
4. Compara cada producto con tu perfil de gusto
5. Te dice exactamente qué elegir — y por qué

Todo de forma transparente, honesta, gratuita y sin inventar nada.

---

## Beneficios

- **Aprende tus gustos con el tiempo.** Cuanto más uses la skill, más
  conoce el agente tu paladar. Cada interacción refina el perfil.

- **Cervezas y vinos en una sola skill.** No necesitas instalar dos skills
  separadas. El agente maneja ambas categorías, reconociendo automáticamente
  lo que está analizando.

- **Análisis desde imágenes y texto.** Toma una foto de un estante, un menú,
  una carta de vinos. O escribe una lista. El agente extrae solo
  los productos relevantes (cervezas y vinos), ignorando todo lo demás.

- **Sin alucinaciones.** El agente tiene la prohibición absoluta de usar
  su propio conocimiento de preentrenamiento. Cada producto es
  investigado rápidamente en la web antes de ser evaluado.

- **Índice de preferencia 0-100%.** Cada sugerencia tiene una puntuación
  clara que indica qué tan bien se adapta un producto a tus gustos. Sin
  medias tintas.

- **Perfil de gusto persistente.** Tus preferencias se guardan en
  archivos de texto legibles y editables. No se pierden entre
  una sesión y la siguiente.

- **Configuración guiada por el agente.** La primera vez, el agente te hace las
  preguntas adecuadas para entender tus gustos, sin dejarte frente a
  configuraciones manuales.

- **Código abierto, licencia MIT.** Gratuito, sin suscripciones, sin
  claves API, sin límites. Puedes usarlo, modificarlo, distribuirlo.

- **Funciona con cualquier agente de IA.** Escrito para OpenCode, pero
  fácilmente convertible para OpenClaw, Hermes Agent, Claude Code, Cursor,
  GitHub Copilot y cualquier otro agente. Muestra este README a tu
  agente para una conversión simple y automática.

- **Totalmente personalizable.** SKILL.md es un archivo de texto.
  Añade reglas, modifica criterios, adáptalo a tu flujo de trabajo.

---

⭐ **¿Te gusta drinks-sommelier?** Pon una estrella, sigue el proyecto
y ayuda a que crezca. Las mejores recomendaciones son las que se
comparten — sugerencias y contribuciones siempre son bienvenidas.

---

## Cómo funciona

El proceso se divide en 5 fases, ejecutadas en secuencia por el agente cada
vez que es consultado.

### Fase 1 — Configuración del perfil de gusto (una sola vez)

La primera vez que se carga la skill, el agente verifica si los
párrafos "Gustos del usuario para cervezas" y "Gustos del usuario para
vinos" en SKILL.md ya han sido completados.

Si no lo han sido, el agente abre el archivo `data/SETUP.md` que contiene:
- Preguntas guía para recopilar preferencias (dulce/amargo, graduación alcohólica,
  estilos gustados y no gustados, etc.)
- Ejemplos de párrafos correctamente completados
- Ejemplos de archivos `data/` poblados

El agente te hace las preguntas, recopila las respuestas y modifica
los dos párrafos de gusto en SKILL.md. Si durante la
configuración el usuario menciona productos específicos, el agente
los registra en los archivos `data/` correspondientes (operación
opcional pero útil para refinar el perfil).

También puedes completar los párrafos manualmente, si lo prefieres.

Los archivos `data/known-preferred-beers.md` y `data/known-preferred-wines.md`
son opcionales y contienen productos específicos que ya has evaluado
en el pasado. Cuanto más completos estén, más entiende el agente tus matices.

### Fase 2 — Análisis de entrada

El agente identifica lo que tienes disponible y en qué formato:

- **Texto**: extrae los nombres de cervezas y vinos de una lista escrita
- **Imagen**: analiza la foto (estante, menú, carta de vinos) y
  reconoce solo productos que sean cervezas o vinos.
  Ignora completamente: licores, destilados, aperitivos, comidas,
  postres, refrescos, accesorios. Cualquier cosa que no sea cerveza o vino.
- **Mixto**: si envías tanto texto como imágenes, lo analiza todo.

Si la entrada no está clara, el agente pregunta antes de proceder.

### Fase 3 — Investigación web (antialucinaciones)

El agente tiene la **prohibición absoluta** de usar su propio
conocimiento de preentrenamiento para evaluar un producto. Podría estar obsoleto,
ser impreciso o, peor aún, inventado. Por esta razón, realiza una búsqueda web específica
sobre cada uno y todos los productos identificados.

Lo que el agente busca:

| Categoría | Información recopilada |
|---|---|
| **Cervezas** | Estilo, graduación alcohólica, dulzor, amargor (IBU), cuerpo, notas aromáticas, ingredientes |
| **Vinos** | Variedad de uva, denominación, zona de producción, añada, cuerpo, acidez, tanicidad, graduación alcohólica, notas de dulzor |

Si un producto no se encuentra en línea, el agente lo indica honestamente
y no inventa características.

### Fase 4 — Evaluación

El agente compara cada producto con tu perfil de gusto, que tiene
dos niveles distintos:

1. **Reglas de gusto** — las pautas generales que has escrito
   en los párrafos de gusto (p. ej., "cervezas dulces", "vinos no demasiado
   dulces", "graduación alcohólica ≤ 9°"). Son vinculantes.
2. **Productos en archivos data/** — ejemplos concretos de cervezas y vinos
   que te gustaron o no. Sirven para calibrar las
   reglas de gusto (p. ej., si te encanta la cerveza X y odias la Y, el agente
   entiende lo que quieres decir con "dulce" y "amargo").

El agente asigna un **índice de preferencia de 0 a 100%**:

| Índice | Significado |
|---|---|
| 90-100% | Producto perfecto para tus gustos |
| 70-89% | Excelente, ligeras discrepancias |
| 50-69% | Aceptable, pero no óptimo |
| 30-49% | Poco adecuado para tus gustos |
| 0-29% | Evitar |

Si has indicado un contexto alimenticio, el agente también evalúa
el maridaje (prioridad secundaria).

### Fase 5 — Recomendación

El agente estructura la respuesta claramente:

1. **Primera opción**: el mejor producto con índice de preferencia
   y explicación de por qué es adecuado para tus gustos
2. **Alternativas** (si las hay): en orden descendente de preferencia
3. **Maridajes**: sugerencias de maridaje para los productos
4. **Productos a evitar**: aquellos que claramente no respetan
   tus gustos, con explicación

---

## Estructura del proyecto

```
drinks-sommelier/
├── README.md                ← Este archivo
├── LICENSE                  ← Licencia MIT
├── .gitignore
├── img/                     ← Logo y recursos gráficos
├── i18n/                    ← Traducciones
└── skills/
    └── drinks-sommelier/    ← La skill en sí
        ├── SKILL.md         ← Instrucciones completas para el agente
        │                      (frontmatter, gustos, operaciones,
        │                       casos límite, mejores prácticas, ejemplos,
        │                       actualizaciones de preferencias)
        └── data/
            ├── SETUP.md                   ← Guía de configuración inicial
            │                                (se usa solo en el primer inicio)
            ├── known-preferred-beers.md   ← Cervezas gustadas y no gustadas
            │                                (se completa con el uso)
            └── known-preferred-wines.md   ← Vinos gustados y no gustados
                                              (se completa con el uso)
```

---

## Instalación

Puedes instalar la skill de dos maneras:

### Con npx skills (recomendado)

```bash
npx skills add Johell1NS/drinks-sommelier --skill drinks-sommelier
```

### Con git clone

```bash
git clone https://github.com/Johell1NS/drinks-sommelier.git
```

Luego copia (o crea un enlace simbólico) la carpeta `skills/drinks-sommelier/` al
directorio de skills de tu agente.

> **Nota:** a diferencia de `npx skills add`, git clone no sabe dónde
> se almacenan las skills de tu agente. Debes colocar la skill en la ruta
> correcta para tu agente (p. ej., OpenCode usa `~/.config/opencode/skills/`,
> otros agentes pueden diferir). Una vez que está allí, el agente la detecta
> automáticamente.

---

## Configuración

La skill necesita conocer tus gustos para funcionar. Puedes
configurarla de dos maneras:

### Configuración guiada (recomendada)

Después de instalar la skill, pide a tu agente algo como
"Ayúdame a configurar la skill drinks-sommelier". El agente cargará
SKILL.md, encontrará los párrafos de gusto aún por completar y te
guiará a través de la configuración inicial usando `data/SETUP.md`.

Alternativamente, simplemente pide una recomendación de cerveza o vino:
el agente detectará automáticamente que la skill no está inicializada
y te hará las preguntas adecuadas.

### Configuración manual

Abre `SKILL.md` y completa los párrafos:

**Gustos del usuario para cervezas**
```
Prefiero cervezas dulces y no amargas.
No deben superar los 9° de graduación alcohólica.
Me gustan los estilos belgas y las cervezas afrutadas.
No me gustan las IPAs, las stouts ni las cervezas demasiado amargas.
```

**Gustos del usuario para vinos**
```
Prefiero vinos tintos no demasiado dulces.
Para blancos, prefiero vermentino y sauvignon.
Me gustan los vinos con buena acidez y frescura.
No me gustan los vinos passito ni los fortificados.
```

También puedes poblar los archivos `data/known-preferred-beers.md` y
`data/known-preferred-wines.md` con productos específicos que ya hayas
probado y evaluado. Esta parte es opcional pero útil
para refinar el perfil.

**Ejemplo — `data/known-preferred-beers.md`**
```
# CERVEZAS GUSTADAS
- Kwak
- Triple Karmeliet
- La Trappe Blond
- Flea Margherita

# CERVEZAS NO GUSTADAS
- Cualquier IPA
- Stout
- Cervezas con graduación alcohólica superior a 9°
```

**Ejemplo — `data/known-preferred-wines.md`**
```
# VINOS GUSTADOS
- Vermentino Costamolino
- Syrah Soraia Casale Valle Chiesa
- Rebeca Firriato

# VINOS NO GUSTADOS
- Vinos passito
- Vinos fortificados
```

### Actualización con el tiempo

Cada vez que expreses un juicio sobre un producto ("Este me gusta",
"Este no me gusta"), el agente actualiza automáticamente los
archivos `data/`. Las reglas de gusto en los párrafos de SKILL.md, en cambio,
se actualizan solo con tu confirmación explícita, porque
son vinculantes para evaluaciones futuras.

---

## Ejemplos de uso

### Escenario 1 — Estante de vinos (imagen)
Tomas una foto de un estante de una tienda de vinos. El agente identifica los vinos,
los investiga todos en la web, los compara con tu perfil. Te dice
cuál elegir, por qué y con qué maridarlo.

### Escenario 2 — Menú de cervezas (imagen)
Tomas una foto del menú de cervezas de un pub. El agente ignora cócteles,
licores, etc... analiza solo las cervezas, busca información sobre
cada una. Sugiere la cerveza más adecuada para tus gustos.

### Escenario 3 — Lista de texto mixta
Escribes "Tengo estos vinos: Chianti Classico, Vermentino Costamolino,
Amarone. Y estas cervezas: Kwak, IPA artesanal local, Leffe Blonde."
El agente evalúa ambas categorías y te dice cuál es la mejor
opción en general.

### Escenario 4 — Solicitud sin lista
"Necesito conseguir un vino para una cena, ¿qué me recomiendas?" El agente
no inventa. Pregunta qué tienes disponible, qué tipo de cena
y si ya tienes algún vino en mente.

### Escenario 5 — Nueva preferencia expresada
Después de una sugerencia dices "Esa cerveza me gustó mucho".
El agente la añade a tus favoritos y actualiza el perfil
para ser aún más preciso la próxima vez.

---

## Lo que esta skill NO hace

- **No proporciona evaluaciones de cata profesionales.** Las
  sugerencias se basan en datos objetivos (estilo, graduación alcohólica,
  amargor) y en preferencias declaradas. No reemplaza a un
  sommelier humano en contextos formales.

- **No maneja otras bebidas.** Licores, destilados, cócteles,
  refrescos, bebidas no alcohólicas — cualquier cosa que no sea cerveza o vino se
  ignora.

---

## Sugerencias (opcional)

**drinks-sommelier** funciona con cualquier herramienta de búsqueda web que tu agente
soporte de forma nativa. Si tu agente ya tiene capacidades de búsqueda web fiables,
no necesitas nada más.

Sin embargo, si quieres asegurar búsquedas exhaustivas y resistentes a antibots
cada vez (especialmente útil cuando las páginas de productos están detrás de sistemas antibot),
considera instalar la skill complementaria
**[browser-search](https://github.com/Johell1NS/browser-search)**.
Busca en decenas de motores simultáneamente y ayuda al agente a encontrar
información de productos incluso cuando las herramientas estándar tienen dificultades.

---

## Licencia
MIT
