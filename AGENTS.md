# Instrucciones para escribir la documentación de Oden Food

Sitio de documentación en [Mintlify](https://mintlify.com). Las páginas son MDX
con frontmatter YAML y la navegación vive en `docs.json`. Se publica solo al
hacer push a `main`.

## Quién lee esto, y por qué importa

Dos públicos, y el segundo sorprende:

1. **Restauranteros**, buscando cómo hacer algo en la app.
2. **El agente de soporte de WhatsApp de Oden.** Lee este sitio en vivo: baja
   `llms.txt` para saber qué guías existen y luego abre la que necesita para
   contestarle a un cliente. Lo que se escriba aquí sale por WhatsApp, casi
   textual, a un restaurantero real.

La consecuencia práctica del segundo: **un dato repartido en varios archivos es
un dato que el agente reconstruye mal, y una media verdad aquí sale por WhatsApp
como una instrucción entera.**

Pasó el 2026-08-28, y la lección no es la que parecía. El bot le dijo a un
cliente que los comanderos entran con PIN, y la documentación afirmaba lo
contrario ("no un PIN") en una tabla. Al revisarlo contra el código, **el bot
tenía razón**: el mesero sí entra con su PIN, sólo que después de vincular el
aparato con un código. La tabla decía "no un PIN" para señalar que el PIN por sí
solo no alcanza, y esa abreviación se leyó como una negación.

Dos reglas salen de ahí:

- Cuando un tema se explica en más de dos lugares, merece guía propia.
- **No abrevies una secuencia en una negación.** "No es un PIN, es un código" se
  convierte en una instrucción falsa. Escribe el orden completo: primero el
  código vincula el aparato, después el PIN identifica a la persona.

## Idioma y tono

- **Todo en español de México, con tuteo.** "Tu restaurante", "tus meseros",
  nunca "su negocio" ni "usted".
- Voz activa, una idea por oración.
- Sin anglicismos innecesarios. Los términos que el producto sí usa en inglés
  se quedan (KDS, PIN), y se explican la primera vez que aparecen en una guía.
- Nada de em-dashes (—). Usa comas, dos puntos, paréntesis o punto y seguido.

## Terminología: las palabras que no se pueden cambiar

El producto se llama **Oden Food**. Nunca "Oden POS" (ése es el nombre interno
del número de WhatsApp que manda los códigos, no el del producto), ni "Oden Pos".

### Las tres formas de acceso, que se confunden todo el tiempo

Ésta es la distinción que más daño hace cuando se explica mal, porque el que la
lee mal se queda sin poder trabajar:

| Forma | Quién | Cómo entra |
|---|---|---|
| **Empleado con PIN** | usa la terminal del negocio (iPad o tablet) | su **PIN de 4 dígitos** |
| **Comandero** | el mesero, desde **su propio celular** | **código de 6 caracteres o QR**, desde Configuración → Operación → Comanderos |
| **Turno / asistencia** | registrar entrada y salida | se registra solo, al entrar con su PIN |

Las dos primeras son una secuencia, no una disyuntiva: el código vincula el
**aparato** (una vez, y expira a las **24 horas**), y después cada mesero entra
en ese aparato con **su** PIN. Un mesero con PIN pero sin celular vinculado no
entra, y un celular vinculado sin empleados dados de alta no tiene con qué PIN
entrar.

Un celular sin vincular NO dice "restringido": muestra la pantalla de vincular y
pide el código. "Acceso restringido" y "sin permisos" son mensajes de **rol**, y
quien los ve tiene el celular funcionando y le falta un permiso.

### Otros nombres que van tal cual

| Se escribe así | No así |
|---|---|
| **Nueva venta** (v minúscula, como en la app) | "Nueva Venta", "nueva orden", "nuevo pedido" |
| **Enviar a cocina** | "mandar a cocina" |
| pantalla de cocina (**KDS**) | "pantalla de chef", "display" |
| **turno de caja** | "corte", "sesión de caja" |
| **comandero** | "mesero móvil", "app del mesero" |
| **mi.oden.food/onboarding** | cualquier otra URL de registro |

Las rutas del menú van con flecha y en negritas, con los niveles completos:
**Configuración → Operación → Comanderos**. Un nivel de menos deja al lector
buscando en una pantalla que no es.

**Hay dos productos con menús distintos, y confundirlos es el error más fácil de
cometer.** La app (iPad o celular) tiene Configuración con categorías y
pestañas; el panel web de mi.oden.food tiene un menú lateral plano. La misma
función se llama distinto en cada uno: en la app se regenera un código con
**Regenerar Código** y en el panel con **Nuevo código**. Antes de citar un botón
o una ruta, decide de cuál de los dos hablas, y dilo. Si la guía cubre los dos,
sepáralos en secciones.

## Estilo de escritura

- Sentence case en los encabezados.
- Negritas para elementos de la interfaz: toca **Empleados**.
- `Código` para nombres de archivo, comandos y rutas técnicas.
- Los títulos del frontmatter son largos y descriptivos a propósito, porque
  cargan el SEO: "Agrega empleados, roles y PIN de acceso en Oden Food", no
  "Empleados".
- Cada guía abre con una línea de `description` que resume qué resuelve.

### Componentes que ya usa este sitio

`<Steps>` y `<Step>` para procedimientos, `<Accordion>` y `<AccordionGroup>`
para preguntas frecuentes, `<Note>` para contexto, `<Tip>` para atajos,
`<Warning>` para lo que puede salir caro, `<Card>` y `<CardGroup>` para índices.
No introduzcas un componente nuevo si uno de éstos hace el trabajo.

## Qué no se documenta aquí

- Pantallas internas de administración (el back-office de Automatic73, sunny).
- Precios negociados, descuentos puntuales o acuerdos con un cliente concreto.
- Números de teléfono internos, ids de WhatsApp, tokens o nombres de secretos.
  **Este repositorio es público.**
- Funciones a medio construir. Si no está en producción, no está en la doc: el
  agente de soporte la va a leer y a prometérsela a un cliente.

## Antes de abrir un PR

- La página nueva tiene que estar en `docs.json`, o no aparece en la navegación
  (y entonces tampoco en `llms.txt`, así que el agente de soporte no la ve).
- Los enlaces internos van con ruta relativa desde la raíz: `/setup/employees`.
- Si el cambio corrige algo que el agente estaba explicando mal, dilo en el PR:
  es la señal de que hay que volver a probarlo por WhatsApp.
