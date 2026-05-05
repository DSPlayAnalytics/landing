# DSPlay Analytics — Landing

Landing comercial do [DSPlay Analytics](https://dsplayground.com.br), construída com Astro 6 + Tailwind 4. Inclui área pública (marketing, preços, integrações) e área autenticada do cliente (painel, configurações, exportação de dados).

## Stack

- [Astro 6](https://astro.build) — geração estática + SSR
- [Tailwind CSS 4](https://tailwindcss.com) — tokens via `@theme {}` em `src/styles/global.css`
- [DSPlay Analytics SDK](https://github.com/DSPlayAnalytics/SDK) — telemetria de funil (dogfood)
- Deploy via [Cloudflare Pages](https://pages.cloudflare.com)

## Páginas

| Rota | Descrição |
|---|---|
| `/` | Home |
| `/precos` | Planos free / pro |
| `/recursos` | Funcionalidades |
| `/integracoes` | Guias de integração |
| `/seguranca` | Política de segurança |
| `/sobre` | Sobre o projeto |
| `/changelog` | Histórico de versões |
| `/status` | Status da plataforma |
| `/cliente/cadastro` | Criação de conta |
| `/cliente/login` | Login |
| `/cliente/painel` | Dashboard do cliente (autenticado) |
| `/cliente/configuracoes` | Configurações — 7 abas |
| `/cliente/onboarding` | Wizard de onboarding — 3 passos |
| `/cliente/exportar` | Download de dados arquivados |
| `/cliente/esqueci-senha` | Recuperação de senha |

## Design system

Componentes em `src/components/ui/`:

`Badge` · `Breadcrumbs` · `Button` · `Card` · `ChartCard` · `EmptyState` · `FormError` · `Input` · `MetricCard` · `Section` · `Stepper` · `Tabs` · `ToastContainer`

Tokens semânticos (`success`, `warning`, `danger`, `info`) definidos em `src/styles/global.css` via `@theme {}`.

## Desenvolvimento local

### Pré-requisitos

- Node.js 20+
- Backend rodando em `http://localhost:5000` ([DSPlayAnalytics/backend](https://github.com/DSPlayAnalytics/backend))

### Instalação

```bash
npm install
cp .env.example .env
# Ajuste PUBLIC_API_URL=http://localhost:5000 para dev local
```

### Comandos

```bash
npm run dev        # servidor de desenvolvimento (http://localhost:4321)
npm run build      # build estático para ./dist
npm run preview    # preview do build
npm run check      # astro check + tsc
npm run test       # vitest (245 testes)
```

## Variáveis de ambiente

Todas as variáveis são públicas (embutidas no bundle em build time):

| Variável | Descrição | Padrão |
|---|---|---|
| `PUBLIC_SITE_URL` | URL canônica do site | `https://dsplayground.com.br` |
| `PUBLIC_API_URL` | URL do backend de auth/ingest | `https://api.dsplayground.com.br` |
| `PUBLIC_DASHBOARD_URL` | URL base do dashboard logado | `https://app.dsplayground.com.br/cliente/metricas` |
| `PUBLIC_PUBLISHABLE_KEY` | Publishable key da própria landing (dogfood) | vazio |
| `PUBLIC_DEBUG` | Logs do SDK no console | `false` |

## Deploy

O deploy é gerenciado pelo Cloudflare Pages apontando para este repositório. O build roda automaticamente em cada push para `main`.

```
astro build → dist/ → Cloudflare Pages CDN
```

## Licença

MIT
