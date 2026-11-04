<div align="center">
  <img src="https://github.com/Nucleify/Nucleify/blob/prod/public/img/logo.svg" width="88" alt="Nucleify" />
  <h1>Nucleify</h1>
  <p><strong>Silnik Kompilacji IR i Automatycznej Migracji Frameworków dla TypeScript</strong></p>
  <p>Pisz stan, walidację i logikę domenową raz w czystym TypeScript. Emituj w 100% czytelny, idiomatyczny kod dla Next.js, Nuxt, Astro, Svelte i Solid.</p>

  <p>
    <a href="https://nucleify.io">Strona Główna</a> •
    <a href="https://docs.nucleify.io">Dokumentacja</a> •
    <a href="https://ui.nucleify.io">nucleify-ui</a>
  </p>
</div>

---

Co 3 lata branżę frontendową zalewa kolejna fala zmian: z Vue 2 na Vue 3, ze starych SPA na Next.js App Router, lub z Reacta na Svelte i Astro pod wymogi wydajnościowe.

Ręczne przepisywanie frontendu zamraża roadmapę produktową na 3–6 miesięcy i pochłania setki tysięcy dolarów na powtórną implementację tych samych formularzy, sesji i maszyn stanowych.

**Nucleify rozwiązuje ten problem:**
- **Pojedyncze Źródło Prawdy (`shared_modules`)**: Logika biznesowa, stan reaktywny i kontrakty API żyją w czystym TypeScript bez frameworkowych wrapperów.
- **Silnik Kompilacji Intermediate Representation (IR)**: Parsuje AST i tłumaczy logikę na natywne idiomy frameworka (React hooks, Vue composables, Svelte runes).
- **Zero Runtime Overhead**: Brak jakichkolwiek bibliotek runtime pośredniczących w paczce produkcyjnej (`@nucleify/runtime` nie trafia do Twojego bundla).
- **Zero Vendor Lock-In**: Jesteś właścicielem 100% wygenerowanego kodu. Jeśli jutro odłączysz się od Nucleify, Twój projekt buduje się i deployuje jak każdy standardowy projekt Next.js, Nuxt czy Svelte.

---

## Obsługiwane Frameworki Docelowe

| Framework | Flaga Celu | Generowane Idiomy |
|---|---|---|
| **Next.js** | `--target=next` | React 19 App Router, `'use client'`, natywne hooki (`useState`, `useEffect`) |
| **Nuxt** | `--target=nuxt` | Vue 3.5, `<script setup lang="ts">`, `ref()`, auto-importy |
| **Svelte** | `--target=svelte` | Składnia Svelte 5 Runes (`$state`, `$derived`, `$props`) |
| **Astro** | `--target=astro` | Szablony statyczne / SSR, architektura wysp (islands) bez zbędnego JS |
| **Solid.js** | `--target=solid` | Drobnoziarnista reaktywność, sygnały (`createSignal`) |

---

## Szybki Start

```bash
# Sklonuj repozytorium
git clone https://github.com/Nucleify/Nucleify.git
cd Nucleify

# Przygotuj środowisko i zależności
make run

# Uruchom kanoniczny serwer Nuxt (http://localhost:7777)
make web

# Konwertuj i uruchom na innym frameworku:
make web TARGET=next     # Konwertuje i uruchamia aplikację Next.js
make web TARGET=svelte   # Konwertuje i uruchamia aplikację Svelte
```

---

## Porównanie Jakości Kodu

### Źródło: Czysty TypeScript (`src/modules/auth/user-session.ts`)
```typescript
import { state, handler } from '#nuc-compiler/runtime'

export const userSession = {
  email: state(''),
  isLoading: state(false),
  login: handler(async (email: string) => {
    // Czysta logika biznesowa
  })
}
```

### Wyemitowany Next.js (`components/UserSession.tsx`)
```tsx
'use client'
import { useState } from 'react'

export function UserSession() {
  const [email, setEmail] = useState('')
  const [isLoading, setIsLoading] = useState(false)
  // W 100% czysty React. Zero obcych zależności Nucleify w runtime.
}
```

### Wyemitowany Nuxt 3 (`components/UserSession.vue`)
```vue
<script setup lang="ts">
const email = ref('')
const isLoading = ref(false)
// W 100% natywne composables Vue 3.
</script>
```

---

## Architektura w Skrócie

```txt
nucleify/
├── web/                    # Kanoniczna aplikacja Nuxt 4 (landing)
├── admin/                  # Kanoniczny panel administracyjny Nuxt 4
├── docs/                   # Serwis dokumentacji Astro 5
├── compiler/               # Rdzeń kompilatora IR AST
├── shared_modules/         # Moduły funkcjonalne (API, Auth, Kolory, i18n, Stores)
├── portable/nui/           # Tokeny stylów i web komponenty UI
└── supabase/               # Migracje, seedery i funkcje bazy PostgreSQL
```

---

## Wsparcie Komercyjne & Usługi Migracji (B2B)

- **Redukcja Kosztu Migracji o 70%**: Skróć wielomiesięczny refactoring do 2–3 tygodni zautomatyzowanej kompilacji IR.
- **Darmowe PoC (Proof of Concept)**: Prześlij nam 3–5 typowych komponentów ze swojego projektu, a w 48 godzin odeślemy Ci działający, idiomatyczny kod w wybranym frameworku docelowym.
- **Enterprise On-Premises & Code Escrow**: Uruchom kompilator lokalnie w infrastrukturze air-gapped z pełnym zabezpieczeniem prawnym depozytu kodu źródłowego.

Kontakt: [team@nucleify.io](mailto:team@nucleify.io) • Strona: [nucleify.io](https://nucleify.io)

---

## Licencja

Moduły bazowe i open-core udostępniane są na licencji MIT. Narzędzia kompilacji zaawansowanej i migracji enterprise objęte są licencją komercyjną Nucleify.
