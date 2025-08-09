# MisPatitas-con-chat-gpt
# 📦 Mis Patitas — Repo Base (Next.js 14 + Tailwind + Supabase)

> Copia estos archivos tal cual en un repositorio nuevo (GitHub) y luego **Import to Vercel**. Solo debes poner tus variables de entorno y listo.

---

## package.json
```json
{
  "name": "mis-patitas",
  "private": true,
  "version": "0.1.0",
  "scripts": {
    "dev": "next dev",
    "build": "next build",
    "start": "next start",
    "lint": "next lint"
  },
  "dependencies": {
    "@supabase/supabase-js": "^2.45.4",
    "framer-motion": "^11.0.0",
    "lucide-react": "^0.454.0",
    "next": "^14.2.5",
    "react": "^18.3.1",
    "react-dom": "^18.3.1"
  },
  "devDependencies": {
    "@types/node": "^20.11.30",
    "@types/react": "^18.2.66",
    "@types/react-dom": "^18.2.22",
    "autoprefixer": "^10.4.19",
    "eslint": "^8.57.0",
    "eslint-config-next": "^14.2.5",
    "postcss": "^8.4.38",
    "tailwindcss": "^3.4.4",
    "typescript": "^5.4.5"
  }
}
```

---

## next.config.ts
```ts
import type { NextConfig } from 'next';

const nextConfig: NextConfig = {
  reactStrictMode: true,
  experimental: {
    optimizePackageImports: ['lucide-react']
  }
};

export default nextConfig;
```

---

## tsconfig.json
```json
{
  "compilerOptions": {
    "target": "es2020",
    "lib": ["dom", "dom.iterable", "esnext"],
    "allowJs": false,
    "skipLibCheck": true,
    "strict": true,
    "noEmit": true,
    "esModuleInterop": true,
    "module": "esnext",
    "moduleResolution": "bundler",
    "resolveJsonModule": true,
    "isolatedModules": true,
    "jsx": "preserve",
    "plugins": [{ "name": "next" }]
  },
  "include": ["next-env.d.ts", "**/*.ts", "**/*.tsx"],
  "exclude": ["node_modules"]
}
```

---

## postcss.config.js
```js
module.exports = {
  plugins: {
    tailwindcss: {},
    autoprefixer: {},
  },
};
```

---

## tailwind.config.ts
```ts
import type { Config } from 'tailwindcss';

const config: Config = {
  darkMode: ['class'],
  content: [
    './app/**/*.{ts,tsx}',
    './components/**/*.{ts,tsx}',
    './pages/**/*.{ts,tsx}',
  ],
  theme: {
    extend: {},
  },
  plugins: [],
};
export default config;
```

---

## app/layout.tsx
```tsx
import './globals.css';
import type { Metadata } from 'next';

export const metadata: Metadata = {
  title: 'Mis Patitas',
  description: 'Marketplace de servicios y productos para mascotas',
};

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="es">
      <body className="min-h-screen bg-gradient-to-b from-amber-50 via-white to-white text-slate-800">
        {children}
      </body>
    </html>
  );
}
```

---

## app/page.tsx (Landing)
```tsx
'use client';
import { motion } from 'framer-motion';
import { PawPrint, Search, Star, Phone, Calendar, MessageCircle, Store, Dog, Scissors, ShieldCheck, MapPin } from 'lucide-react';

export default function Home() {
  return (
    <div>
      <Header />
      <main className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
        <Hero />
        <QuickSearch />
        <Categories />
        <FeaturedMock />
        <HowItWorks />
      </main>
      <Footer />
    </div>
  );
}

function Header() {
  return (
    <div className="sticky top-0 z-40 backdrop-blur bg-white/70 border-b">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 h-16 flex items-center justify-between">
        <div className="flex items-center gap-3">
          <div className="p-2 rounded-2xl bg-amber-100 text-amber-700 shadow-sm">
            <PawPrint className="w-6 h-6" />
          </div>
          <span className="font-extrabold text-xl tracking-tight">Mis Patitas</span>
          <span className="hidden md:inline-block text-xs px-2 py-1 rounded-full bg-emerald-100 text-emerald-700 ml-2">Marketplace</span>
        </div>
        <nav className="hidden md:flex items-center gap-6 text-sm">
          <a className="hover:text-amber-700" href="#explorar">Explorar</a>
          <a className="hover:text-amber-700" href="/live">En vivo</a>
          <a className="hover:text-amber-700" href="#como-funciona">Cómo funciona</a>
        </nav>
        <div className="flex items-center gap-2">
          <a href="#login" className="text-sm font-medium px-3 py-2 rounded-xl hover:bg-slate-100">Ingresar</a>
          <a href="#registro" className="text-sm font-semibold px-4 py-2 rounded-xl bg-amber-600 text-white hover:bg-amber-700 shadow">Crear cuenta</a>
        </div>
      </div>
    </div>
  );
}

function Hero() {
  return (
    <section className="py-12 sm:py-16 lg:py-20">
      <div className="grid lg:grid-cols-2 gap-10 items-center">
        <motion.div initial={{ opacity: 0, y: 12 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 0.6 }}>
          <h1 className="text-3xl sm:text-4xl lg:text-5xl font-extrabold leading-tight">
            Encuentra paseadores, adiestradores y tiendas <span className="text-amber-700">de confianza</span>
          </h1>
          <p className="mt-4 text-slate-600 text-lg">Perfiles verificados, agenda visible y contacto directo por WhatsApp o llamada.</p>
          <div className="mt-6 flex flex-wrap gap-3">
            <a href="#explorar" className="px-5 py-3 rounded-2xl bg-slate-900 text-white hover:bg-slate-800 font-semibold shadow">Explorar ahora</a>
            <a href="#ser-proveedor" className="px-5 py-3 rounded-2xl bg-amber-100 text-amber-800 hover:bg-amber-200 font-semibold">Quiero ofrecer servicios</a>
          </div>
          <div className="mt-6 flex items-center gap-4 text-sm text-slate-500">
            <div className="flex items-center gap-1"><ShieldCheck className="w-4 h-4 text-emerald-600"/> Verificación básica</div>
            <div className="flex items-center gap-1"><Calendar className="w-4 h-4 text-amber-600"/> Calendario público</div>
            <div className="flex items-center gap-1"><Phone className="w-4 h-4 text-sky-600"/> Contacto directo</div>
          </div>
        </motion.div>
        <motion.div initial={{ opacity: 0, y: 12 }} animate={{ opacity: 1, y: 0 }} transition={{ duration: 0.6, delay: 0.1 }}>
          <div className="relative">
            <div className="aspect-[4/3] rounded-3xl bg-gradient-to-br from-amber-200 to-rose-100 shadow-inner overflow-hidden">
              <div className="absolute inset-0 grid grid-cols-2 gap-4 p-6">
                <MockCard name="Paseo 60min" provider="Lau Walks" rating={4.9} price="S/ 35" tags={["Miraflores","Seguro","24h"]} />
                <MockCard name="Baño y corte" provider="Oh My Pet" rating={4.7} price="S/ 60" tags={["A domicilio","Higiene"]} />
                <MockCard name="Adiestramiento básico" provider="CanEdu" rating={5.0} price="S/ 120" tags={["Cachorros","Clicker"]} />
                <MockCard name="Juguete mordedor" provider="DogStore" rating={4.6} price="S/ 22" tags={["Envío 24h","Eco"]} />
              </div>
            </div>
          </div>
        </motion.div>
      </div>
    </section>
  );
}

function MockCard({ name, provider, rating, price, tags }: { name: string; provider: string; rating: number; price: string; tags: string[] }) {
  return (
    <div className="bg-white rounded-2xl p-4 shadow-sm border">
      <div className="flex items-start justify-between">
        <div>
          <p className="font-semibold text-slate-800">{name}</p>
          <p className="text-xs text-slate-500">por {provider}</p>
        </div>
        <div className="flex items-center gap-1 text-amber-600"><Star className="w-4 h-4" /><span className="text-sm font-semibold">{rating}</span></div>
      </div>
      <div className="mt-3 flex flex-wrap gap-2">
        {tags.map((t) => (
          <span key={t} className="text-xs px-2 py-1 rounded-full bg-slate-100 text-slate-600">{t}</span>
        ))}
      </div>
      <div className="mt-4 flex items-center justify-between">
        <span className="font-bold">{price}</span>
        <div className="flex items-center gap-2 text-slate-500">
          <MessageCircle className="w-4 h-4"/>
          <Phone className="w-4 h-4"/>
        </div>
      </div>
    </div>
  );
}

function QuickSearch() {
  return (
    <section id="explorar" className="mb-12">
      <div className="rounded-3xl bg-white shadow ring-1 ring-slate-200 p-4 md:p-6">
        <div className="flex flex-col md:flex-row gap-3 items-stretch">
          <div className="flex-1 flex items-center gap-3 bg-slate-50 rounded-2xl px-3 py-2">
            <Search className="w-5 h-5 text-slate-500"/>
            <input className="bg-transparent outline-none w-full text-sm" placeholder="Busca paseadores, adiestradores, baño…"/>
          </div>
          <div className="grid grid-cols-2 sm:grid-cols-3 gap-2">
            <button className="px-4 py-2 rounded-xl bg-slate-900 text-white text-sm font-semibold">Hoy</button>
            <button className="px-4 py-2 rounded-xl bg-slate-100 text-slate-700 text-sm">Esta semana</button>
            <button className="px-4 py-2 rounded-xl bg-slate-100 text-slate-700 text-sm">Miraflores</button>
          </div>
        </div>
      </div>
    </section>
  );
}

function Categories() {
  const items = [
    { icon: Dog, label: 'Paseo', desc: 'Caminatas seguras y reportes.' },
    { icon: Scissors, label: 'Grooming', desc: 'Baño, corte e higiene.' },
    { icon: Store, label: 'Tiendas', desc: 'Accesorios y alimentos.' },
    { icon: ShieldCheck, label: 'Adiestramiento', desc: 'Obediencia y conducta.' },
  ];
  return (
    <section id="categorias" className="py-6">
      <h2 className="text-xl font-bold mb-4">Categorías</h2>
      <div className="grid sm:grid-cols-2 lg:grid-cols-4 gap-4">
        {items.map(({ icon: Icon, label, desc }) => (
          <div key={label} className="rounded-2xl border bg-white p-5 hover:shadow-sm transition">
            <div className={`w-10 h-10 rounded-xl bg-slate-900/5 text-slate-900 flex items-center justify-center mb-3`}>
              <Icon className="w-5 h-5"/>
            </div>
            <div className="font-semibold">{label}</div>
            <div className="text-sm text-slate-600">{desc}</div>
          </div>
        ))}
      </div>
    </section>
  );
}

function FeaturedMock() {
  const providers = [
    { name: 'Lau Walks', type: 'Paseadora', rating: 4.9, location: 'Miraflores, Lima' },
    { name: 'CanEdu', type: 'Adiestramiento', rating: 5.0, location: 'Surco, Lima' },
    { name: 'Oh My Pet', type: 'Grooming', rating: 4.7, location: 'San Borja, Lima' },
  ];
  return (
    <section className="py-8">
      <div className="flex items-center justify-between mb-4">
        <h2 className="text-xl font-bold">Destacados cerca de ti</h2>
        <a className="text-sm text-amber-700 font-semibold" href="/live">Ver en vivo</a>
      </div>
      <div className="grid md:grid-cols-3 gap-4">
        {providers.map((p) => (
          <div key={p.name} className="rounded-2xl border bg-white p-5 hover:shadow-sm transition">
            <div className="flex items-start justify-between">
              <div>
                <div className="font-semibold text-slate-900 flex items-center gap-2">{p.name}<span className="text-xs px-2 py-1 rounded-full bg-slate-100 text-slate-600">{p.type}</span></div>
                <div className="text-sm text-slate-500 flex items-center gap-1 mt-1"><MapPin className="w-4 h-4"/>{p.location}</div>
              </div>
              <div className="flex items-center gap-1 text-amber-600"><Star className="w-4 h-4"/><span className="text-sm font-semibold">{p.rating}</span></div>
            </div>
            <div className="mt-4 flex items-center justify-end gap-2">
              <a className="px-3 py-2 rounded-xl bg-emerald-600 text-white text-sm font-semibold hover:bg-emerald-700" href="#whatsapp">WhatsApp</a>
              <a className="px-3 py-2 rounded-xl bg-slate-900 text-white text-sm font-semibold hover:bg-slate-800" href="#perfil">Ver perfil</a>
            </div>
          </div>
        ))}
      </div>
    </section>
  );
}

function HowItWorks() {
  const steps = [
    { icon: Search, title: 'Explora', desc: 'Filtra por zona, categoría, precio y disponibilidad.' },
    { icon: Calendar, title: 'Agenda', desc: 'Elige día y hora visibles en el calendario del proveedor.' },
    { icon: Phone, title: 'Contacta', desc: 'Habla por WhatsApp/llamada para ultimar detalles.' },
    { icon: Star, title: 'Valora', desc: 'Deja una reseña tras completar el servicio.' },
  ];
  return (
    <section id="como-funciona" className="py-10">
      <h2 className="text-xl font-bold mb-4">¿Cómo funciona?</h2>
      <div className="grid md:grid-cols-4 gap-4">
        {steps.map(({ icon: Icon, title, desc }) => (
          <div key={title} className="rounded-2xl border bg-white p-5">
            <div className="w-10 h-10 rounded-xl bg-slate-900 text-white flex items-center justify-center mb-3">
              <Icon className="w-5 h-5"/>
            </div>
            <div className="font-semibold">{title}</div>
            <div className="text-sm text-slate-600">{desc}</div>
          </div>
        ))}
      </div>
    </section>
  );
}

function Footer() {
  return (
    <footer className="mt-16 border-t">
      <div className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10 grid md:grid-cols-4 gap-8 text-sm">
        <div>
          <div className="flex items-center gap-2 font-bold text-slate-900"><PawPrint className="w-5 h-5"/> Mis Patitas</div>
          <p className="mt-2 text-slate-500">Conectamos familias y proveedores de confianza para el bienestar de sus mascotas.</p>
        </div>
        <div>
          <div className="font-semibold mb-2">Explorar</div>
          <ul className="space-y-1 text-slate-600">
            <li><a href="#categorias" className="hover:text-amber-700">Categorías</a></li>
            <li><a href="/live" className="hover:text-amber-700">En vivo</a></li>
          </ul>
        </div>
        <div>
          <div className="font-semibold mb-2">Proveedores</div>
          <ul className="space-y-1 text-slate-600">
            <li><a href="#ser-proveedor" className="hover:text-amber-700">Crear perfil</a></li>
            <li><a href="#" className="hover:text-amber-700">Centro de ayuda</a></li>
          </ul>
        </div>
        <div>
          <div className="font-semibold mb-2">Legal</div>
          <ul className="space-y-1 text-slate-600">
            <li>Términos</li>
            <li>Privacidad</li>
            <li>Cookies</li>
          </ul>
        </div>
      </div>
      <div className="py-6 text-center text-xs text-slate-500">© {new Date().getFullYear()} Mis Patitas. Todos los derechos reservados.</div>
    </footer>
  );
}
```

---

## app/live/page.tsx (Realtime conectado)
```tsx
'use client';
import { useEffect, useState } from 'react';
import { createClient } from '@supabase/supabase-js';
import { PawPrint, Star, Phone, MessageCircle, MapPin, RefreshCcw } from 'lucide-react';

const supabaseUrl = process.env.NEXT_PUBLIC_SUPABASE_URL!;
const supabaseAnon = process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!;
const supabase = createClient(supabaseUrl, supabaseAnon);

type ProviderCardDTO = {
  id: string;
  store_name: string;
  slug: string;
  type: string; // enum provider_type
  city: string | null;
  rating_avg: number | null;
  rating_count: number | null;
};

export default function Live() {
  const [loading, setLoading] = useState(true);
  const [providers, setProviders] = useState<ProviderCardDTO[]>([]);
  const [ts, setTs] = useState<number>(Date.now());

  useEffect(() => {
    let mounted = true;
    async function run() {
      setLoading(true);
      const { data, error } = await supabase
        .from('providers')
        .select('id, store_name, slug, type, city, rating_avg, rating_count')
        .order('rating_avg', { ascending: false })
        .limit(24);
      if (!mounted) return;
      if (error) console.error(error);
      setProviders((data || []) as ProviderCardDTO[]);
      setLoading(false);
    }
    run();
    return () => {
      mounted = false;
    };
  }, [ts]);

  useEffect(() => {
    const channel = supabase
      .channel('providers-realtime')
      .on('postgres_changes', { event: '*', schema: 'public', table: 'providers' }, (payload) => {
        setProviders((prev) => applyRealtime(prev, payload));
      })
      .subscribe();
    return () => {
      supabase.removeChannel(channel);
    };
  }, []);

  return (
    <div>
      <header className="sticky top-0 z-40 backdrop-blur bg-white/70 border-b">
        <div className="max-w-7xl mx-auto h-16 px-4 sm:px-6 lg:px-8 flex items-center justify-between">
          <div className="flex items-center gap-3">
            <div className="p-2 rounded-2xl bg-amber-100 text-amber-700 shadow-sm"><PawPrint className="w-6 h-6" /></div>
            <span className="font-extrabold text-xl tracking-tight">Mis Patitas — En vivo</span>
          </div>
          <button onClick={() => setTs(Date.now())} className="text-sm px-3 py-2 rounded-xl bg-slate-900 text-white flex items-center gap-2">
            <RefreshCcw className="w-4 h-4"/> Recargar
          </button>
        </div>
      </header>

      <main className="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8 py-10">
        <div className="flex items-center justify-between mb-4">
          <h1 className="text-2xl font-extrabold">Proveedores (Realtime)</h1>
          <span className="text-xs text-slate-500">Edita la tabla `providers` en Supabase para ver cambios</span>
        </div>

        {loading ? (
          <SkeletonGrid />
        ) : providers.length === 0 ? (
          <div className="rounded-2xl border bg-white p-6 text-center text-slate-600">
            Aún no hay proveedores. Inserta filas en <code className="px-1 bg-slate-100 rounded">public.providers</code>.
          </div>
        ) : (
          <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-4">
            {providers.map((p) => (
              <ProviderCard key={p.id} p={p} />
            ))}
          </div>
        )}
      </main>
    </div>
  );
}

function ProviderCard({ p }: { p: ProviderCardDTO }) {
  return (
    <div className="rounded-2xl border bg-white p-5 hover:shadow-sm transition">
      <div className="flex items-start justify-between">
        <div>
          <div className="font-semibold text-slate-900 flex items-center gap-2">{p.store_name}
            <span className="text-xs px-2 py-1 rounded-full bg-slate-100 text-slate-600">{p.type}</span>
          </div>
          <div className="text-sm text-slate-500 flex items-center gap-1 mt-1"><MapPin className="w-4 h-4"/>{p.city || '—'}</div>
        </div>
        <div className="flex items-center gap-1 text-amber-600"><Star className="w-4 h-4"/><span className="text-sm font-semibold">{Number(p.rating_avg || 0).toFixed(1)}</span></div>
      </div>
      <div className="mt-4 flex items-center justify-between">
        <a className="px-3 py-2 rounded-xl bg-emerald-600 text-white text-sm font-semibold hover:bg-emerald-700" href={`https://wa.me/51XXXXXXXXX?text=Hola%20${encodeURIComponent(p.store_name)}%20👋`}>WhatsApp</a>
        <div className="flex items-center gap-2 text-slate-500">
          <MessageCircle className="w-4 h-4"/>
          <Phone className="w-4 h-4"/>
        </div>
      </div>
    </div>
  );
}

function SkeletonGrid() {
  return (
    <div className="grid md:grid-cols-2 lg:grid-cols-3 gap-4">
      {Array.from({ length: 6 }).map((_, i) => (
        <div key={i} className="rounded-2xl border bg-white p-5 animate-pulse">
          <div className="h-4 w-2/3 bg-slate-100 rounded mb-2"/>
          <div className="h-3 w-1/3 bg-slate-100 rounded mb-6"/>
          <div className="h-8 w-full bg-slate-100 rounded"/>
        </div>
      ))}
    </div>
  );
}

function applyRealtime(prev: ProviderCardDTO[], payload: any): ProviderCardDTO[] {
  const { eventType, new: newRow, old: oldRow } = payload;
  if (eventType === 'INSERT') return [newRow, ...prev];
  if (eventType === 'UPDATE') return prev.map((r) => (r.id === newRow.id ? { ...r, ...newRow } : r));
  if (eventType === 'DELETE') return prev.filter((r) => r.id !== (oldRow?.id || newRow?.id));
  return prev;
}
```

---

## lib/supabase.ts (opcional, para reutilizar cliente)
```ts
import { createClient } from '@supabase/supabase-js';

export const supabaseBrowser = () => {
  return createClient(
    process.env.NEXT_PUBLIC_SUPABASE_URL!,
    process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
  );
};
```

---

## styles/globals.css
```css
@tailwind base;
@tailwind components;
@tailwind utilities;

html, body { height: 100%; }
```

---

## .env.example
```bash
NEXT_PUBLIC_SUPABASE_URL=
NEXT_PUBLIC_SUPABASE_ANON_KEY=
NEXT_PUBLIC_SITE_URL=http://localhost:3000
```

---

## README.md (cómo importarlo a Vercel)
```md
# Mis Patitas — Repo Base

1) Crea un repositorio en GitHub y copia estos archivos.
2) En Supabase: crea proyecto, pega el SQL de tablas/RLS y habilita Realtime (providers, services, bookings).
3) En Vercel: New Project → Importa este repo → añade env vars:
   - NEXT_PUBLIC_SUPABASE_URL
   - NEXT_PUBLIC_SUPABASE_ANON_KEY
4) Deploy. 
5) Prueba la vista realtime en /live (edita la tabla providers en Supabase y mira los cambios al instante).
```

---

## Notas
- Este repo es **solo frontend conectado** (MVP). Luego añadiré Auth, dashboards y Admin.
- Para imágenes, ajusta tu bucket (`public2`) cuando integremos subida.
- Rendimiento: usa CSR mínimo; en producción migraremos listados a SSR/ISR + Realtime para robustez.
