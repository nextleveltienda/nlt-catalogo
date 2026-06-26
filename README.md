# NLT Catálogo 👕

Catálogo público de ropa para clientes de Next Level Tienda.
Los clientes entran al link, ven los productos, los agregan al carrito y consultan todo junto por WhatsApp.
Vos gestionás todo desde el panel admin con IA para completar los campos automáticamente.

**Versión segura:** usa solo la anon key (pública y segura). No expone ninguna key privada.

---

## Setup (ya hecho ✅)

Lo siguiente ya quedó configurado en Supabase:
- ✅ Tabla `catalogo_productos` con RLS y datos de ejemplo
- ✅ Bucket `fotos-productos` (público)
- ✅ Políticas de Storage para subir/leer/borrar fotos con anon key

---

## Lo que falta antes de subir a GitHub

### 1. Pegar tu anon key

En **`index.html`** y **`admin.html`**, buscá esta línea y pegá tu anon key:

```js
const SUPABASE_ANON_KEY = 'TU_ANON_KEY_AQUI';
```

(La anon key está en Supabase → Settings → API Keys → Legacy → botón "Copy" al lado de `anon public`. Es la misma que ya usás en la NLT app.)

### 2. Cambiar el PIN del admin

En **`admin.html`**:
```js
const PIN_CORRECTO = '1234'; // ← poné tu propio PIN de 4 dígitos
```

### 3. El número de WhatsApp ya está configurado

`5493513083807` — ya está puesto en `index.html`. Si lo querés cambiar, está en:
```js
const WA_NUMBER = '5493513083807';
```

---

## Deploy en Vercel

1. Subí los 4 archivos al repo `nextleveltienda/nlt-catalogo`
2. En vercel.com → New Project → importá el repo → Deploy
3. En Settings → Domains → agregá `catalogo.nlt.com.ar` y configurá el CNAME en tu DNS

---

## Uso diario

**Publicar un producto:**
1. Abrí `catalogo.nlt.com.ar/admin`
2. Ingresá el PIN
3. Tab "Nuevo" → subí fotos → "Analizar con IA" → revisá → "Publicar"

**Gestionar stock:**
- Tab "Productos" → 🚫 marca sin stock, ✅ vuelve a disponible, 🗑 elimina

**Compartir con clientes:**
- Mandales el link `catalogo.nlt.com.ar` por WhatsApp

---

## Cómo funciona el carrito

Los clientes agregan varios productos al carrito y al tocar "Enviar todo por WhatsApp" se abre el chat con un mensaje pre-armado:

> Hola! Vi el catálogo de Next Level Tienda y me interesan estos productos:
> • Buzo oversized beige — $18.500 (talles: M, L)
> • Remera básica negra — $9.000 (talles: S, M, L)
>
> ¿Cómo puedo coordinar el envío a domicilio? 😊

---

## Estructura

```
nlt-catalogo/
├── index.html          ← Catálogo público (clientes)
├── admin.html          ← Panel de gestión (vos, con PIN)
├── vercel.json         ← Config de rutas Vercel
├── supabase-setup.sql  ← SQL ya ejecutado (referencia)
└── README.md
```

## Stack
HTML/CSS/JS puro · Supabase (tabla + Storage) · Anthropic API (IA de fotos) · Vercel
