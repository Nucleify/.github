<div align="center">
  <img src="https://github.com/Nucleify/Nucleify/blob/prod/public/img/logo.svg" width="88" alt="Nucleify" />
  <h1>Nucleify</h1>
  <p><strong>The TypeScript IR Compiler & Framework Migration Engine</strong></p>
  <p>Write state, validation, and domain logic once in clean TypeScript. Emit 100% human-readable, idiomatic code for Next.js, Nuxt, Astro, Svelte, or Solid.</p>

  <p>
    <a href="https://nucleify.io">Website</a> •
    <a href="https://docs.nucleify.io">Documentation</a> •
    <a href="https://ui.nucleify.io">nucleify-ui</a> •
  </p>
</div>

---

Every 3 years, frontend ecosystems force a painful, costly rewrite: Vue 2 to Vue 3, SPAs to Next.js App Router, React to Svelte or Astro for performance. 

Manual rewrites freeze product roadmaps for 3–6 months and burn hundreds of thousands of dollars re-implementing existing forms, sessions, and state machines.

**Nucleify ends that loop:**
- **Single Source of Truth (`shared_modules`)**: Domain logic, state machines, and data contracts live in pure TypeScript with zero framework wrappers.
- **Intermediate Representation (IR) Compiler**: Parses AST and translates logic into idiomatic, native framework idioms (React hooks, Vue composables, Svelte runes).
- **Zero Runtime Overhead**: No intermediate runtime libraries (`@nucleify/runtime` is not required in your production bundle).
- **Zero Vendor Lock-In**: You own 100% of emitted source code. If you disconnect from Nucleify tomorrow, your project builds and deploys as a standard Next.js, Nuxt, Svelte, or Solid app.

---

## Supported Emit Targets

| Framework | Target Flag | Generated Idioms |
|---|---|---|
| **Next.js** | `--target=next` | React 19 App Router, `'use client'`, hooks (`useState`, `useEffect`) |
| **Nuxt** | `--target=nuxt` | Vue 3.5, `<script setup lang="ts">`, `ref()`, auto-imports |
| **Svelte** | `--target=svelte` | Svelte 5 Runes (`$state`, `$derived`, `$props`) |
| **Astro** | `--target=astro` | Static/SSR templates, zero-JS islands architecture |
| **Solid.js** | `--target=solid` | Fine-grained reactivity, signals (`createSignal`) |

---

## Quick Start

```bash
# Clone repository
git clone https://github.com/Nucleify/Nucleify.git
cd Nucleify

# Setup environment and dependencies
make run

# Start canonical Nuxt dev server (http://localhost:7777)
make web

# Emit or run on another target:
make web TARGET=next     # Converts and runs Next.js shell
make web TARGET=svelte   # Converts and runs Svelte shell
```

---

## Code Quality Comparison

### Source: Pure TypeScript (`src/modules/auth/user-session.ts`)
```typescript
import { state, handler } from '#nuc-compiler/runtime'

export const userSession = {
  email: state(''),
  isLoading: state(false),
  login: handler(async (email: string) => {
    // Domain login logic
  })
}
```

### Emitted Next.js (`components/UserSession.tsx`)
```tsx
'use client'
import { useState } from 'react'

export function UserSession() {
  const [email, setEmail] = useState('')
  const [isLoading, setIsLoading] = useState(false)
  // 100% native React code. Zero Nucleify runtime packages.
}
```

### Emitted Nuxt 3 (`components/UserSession.vue`)
```vue
<script setup lang="ts">
const email = ref('')
const isLoading = ref(false)
// 100% native Vue composables.
</script>
```

---

## Architecture at a Glance

```txt
nucleify/
├── web/                    # Canonical Nuxt 4 web app
├── admin/                  # Canonical Nuxt 4 admin panel
├── docs/                   # Astro 5 documentation site
├── compiler/               # Core IR AST compiler engine
├── shared_modules/         # Feature modules (API, Auth, Theme, i18n, Stores)
├── portable/nui/           # Design tokens & portable UI web components
└── supabase/               # Migrations, seeders, and Postgres functions
```

---

## Commercial & Enterprise Migration

- **Reduce Migration Cost by 70%**: Turn 6-month manual rewrites into 2-3 weeks of automated IR compilation.
- **Free Proof of Concept (PoC)**: Send us 3–5 representative components, and we’ll return idiomatic, production-ready emitted code in your target framework within 48 hours.
- **Enterprise On-Premises & Code Escrow**: Run the compiler entirely air-gapped on your infrastructure with full legal escrow protection.

Contact: [team@nucleify.io](mailto:team@nucleify.io) • Website: [nucleify.io](https://nucleify.io)

---

## License

Core packages and modules are licensed under the MIT License. Enterprise compiler extensions and migration tooling are provided under the Nucleify Commercial License.
