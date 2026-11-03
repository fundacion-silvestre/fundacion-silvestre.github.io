# Fundación Silvestre Stallone

Sitio web mobile-first para solicitar ayuda.

## Archivos

```
fundacion-silvestre/
├── index.html          → Página pública
├── admin.html          → Panel de administración
├── css/style.css
├── css/admin.css
├── js/app.js           → Lógica + cantidades editables
├── js/i18n.js          → Traducciones
├── js/admin.js
├── assets/logo.png     → Tu logo
├── assets/favicon.png
└── assets/gallery/     → Fotos de ayuda
```

## Configuración

### 1. Supabase (ya configurado)
URL y clave anon ya están en `js/app.js` y `js/admin.js`.

Si necesitas las tablas de nuevo, en SQL Editor:

```sql
CREATE TABLE IF NOT EXISTS solicitudes (
  id BIGSERIAL PRIMARY KEY,
  nombre TEXT NOT NULL,
  apellido TEXT NOT NULL,
  edad INTEGER NOT NULL,
  telefono TEXT NOT NULL,
  cantidad_ayuda TEXT NOT NULL,
  motivo TEXT NOT NULL,
  metodo_pago TEXT NOT NULL,
  dato_pago TEXT DEFAULT '',
  dias_espera INTEGER,
  idioma TEXT DEFAULT 'es-latam',
  created_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE IF NOT EXISTS mensajes (
  id BIGSERIAL PRIMARY KEY,
  nombre TEXT NOT NULL,
  mensaje TEXT NOT NULL,
  tipo TEXT DEFAULT 'contacto_agente',
  idioma TEXT DEFAULT 'es-latam',
  created_at TIMESTAMPTZ DEFAULT NOW()
);

CREATE TABLE IF NOT EXISTS resenas (
  id BIGSERIAL PRIMARY KEY,
  nombre TEXT NOT NULL,
  estrellas INTEGER NOT NULL DEFAULT 5,
  comentario TEXT NOT NULL,
  aprobada BOOLEAN DEFAULT false,
  idioma TEXT DEFAULT 'es-latam',
  created_at TIMESTAMPTZ DEFAULT NOW()
);

ALTER TABLE solicitudes ENABLE ROW LEVEL SECURITY;
ALTER TABLE mensajes ENABLE ROW LEVEL SECURITY;
ALTER TABLE resenas ENABLE ROW LEVEL SECURITY;

CREATE POLICY "insert_solicitudes" ON solicitudes FOR INSERT TO anon WITH CHECK (true);
CREATE POLICY "select_solicitudes" ON solicitudes FOR SELECT TO anon USING (true);
CREATE POLICY "delete_solicitudes" ON solicitudes FOR DELETE TO anon USING (true);

CREATE POLICY "insert_mensajes" ON mensajes FOR INSERT TO anon WITH CHECK (true);
CREATE POLICY "select_mensajes" ON mensajes FOR SELECT TO anon USING (true);
CREATE POLICY "delete_mensajes" ON mensajes FOR DELETE TO anon USING (true);

CREATE POLICY "insert_resenas" ON resenas FOR INSERT TO anon WITH CHECK (true);
CREATE POLICY "select_resenas" ON resenas FOR SELECT TO anon USING (true);
CREATE POLICY "update_resenas" ON resenas FOR UPDATE TO anon USING (true) WITH CHECK (true);
CREATE POLICY "delete_resenas" ON resenas FOR DELETE TO anon USING (true);
```

### 2. Editar cantidades
En `js/app.js` busca `CONFIG.opcionesCantidad`.  
Cambia `label` (texto) y `dias` (tarifa mostrada).

### 3. Admin
- URL: `/admin.html`
- Contraseña: `stallone2026` (cámbiala en `js/admin.js`)

### 4. WhatsApp
Número: +1 646-814-3870 (en `index.html`)

### 5. Subir a GitHub Pages
Sube todos los archivos a la raíz del repo y activa Pages en branch `main`.
