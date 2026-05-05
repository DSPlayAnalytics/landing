# DSPlay Analytics — Landing

> Site comercial e área do cliente da plataforma [DSPlay Analytics](https://dsplayground.com.br).

![Astro](https://img.shields.io/badge/Astro-6-BC52EE?logo=astro&logoColor=white)
![Tailwind CSS](https://img.shields.io/badge/Tailwind-4-38BDF8?logo=tailwindcss&logoColor=white)
![Cloudflare Pages](https://img.shields.io/badge/Deploy-Cloudflare%20Pages-F38020?logo=cloudflare&logoColor=white)
![Tests](https://img.shields.io/badge/tests-245%20passing-22C55E)
![License](https://img.shields.io/badge/license-MIT-6B7280)

---

## Visão geral

Aplicação estática construída com **Astro 6 + Tailwind CSS 4**, hospedada no edge via **Cloudflare Pages**. Cobre duas superfícies:

- **Marketing** — home, preços, recursos, integrações, segurança, changelog e status
- **Área do cliente** — cadastro, login, onboarding, painel de métricas, configurações e exportação de dados

A telemetria da própria landing é instrumentada via **[@DSPlayAnalytics/SDK](https://github.com/DSPlayAnalytics/SDK)** (dogfood).

---

## Stack

| Camada | Tecnologia |
|---|---|
| Framework | [Astro 6](https://astro.build) — output estático |
| Estilo | [Tailwind CSS 4](https://tailwindcss.com) — tokens via `@theme {}` |
| Analytics | [@DSPlayAnalytics/SDK](https://github.com/DSPlayAnalytics/SDK) |
| Testes | [Vitest 3](https://vitest.dev) + [Happy DOM 20](https://github.com/capricorn86/happy-dom) |
| Deploy | [Cloudflare Pages](https://pages.cloudflare.com) |

---

## Estrutura de páginas

### Público

| Rota | Descrição |
|---|---|
| `/` | Home — proposta de valor e CTA |
| `/precos` | Planos free / pro com comparativo |
| `/recursos` | Funcionalidades da plataforma |
| `/integracoes` | Guias de integração (snippet + SDK) |
| `/seguranca` | Política de segurança e privacidade |
| `/sobre` | Sobre o projeto |
| `/changelog` | Histórico de versões |
| `/status` | Status dos serviços em tempo real |

### Área do cliente (autenticado)

| Rota | Descrição |
|---|---|
| `/cliente/cadastro` | Criação de conta |
| `/cliente/login` | Login com senha ou magic-link |
| `/cliente/esqueci-senha` | Recuperação de senha por e-mail |
| `/cliente/onboarding` | Wizard de 3 passos pós-cadastro |
| `/cliente/painel` | Dashboard de métricas com live counter |
| `/cliente/configuracoes` | Configurações em 7 abas (chaves, plano, billing, etc.) |
| `/cliente/exportar` | Download de dados arquivados (R2) |

---

## Design system

Componentes reutilizáveis em `src/components/ui/`:

`Badge` · `Breadcrumbs` · `Button` · `Card` · `ChartCard` · `EmptyState` · `FormError` · `Input` · `MetricCard` · `Section` · `Stepper` · `Tabs` · `ToastContainer`

Tokens semânticos (`success`, `warning`, `danger`, `info`) definidos em `src/styles/global.css` via `@theme {}` do Tailwind 4.

---

## Desenvolvimento local

### Pré-requisitos

- Node.js 20+
- Backend rodando localmente ([DSPlayAnalytics/backend](https://github.com/DSPlayAnalytics/backend))
- Token GitHub com `read:packages` para instalar o SDK do GitHub Packages

### Instalação

```bash
# Autenticar no GitHub Packages para o SDK
export NODE_AUTH_TOKEN=$(gh auth token)

npm install
cp .env.example .env
# Ajuste PUBLIC_API_URL=http://localhost:5000 para apontar ao backend local
```

### Comandos disponíveis

```bash
npm run dev        # Servidor de desenvolvimento em http://localhost:4321
npm run build      # Build estático → ./dist
npm run preview    # Preview do build gerado
npm run check      # astro check + TypeScript
npm run test       # Vitest — 245 testes
```

---

## Variáveis de ambiente

Todas as variáveis são **públicas** — embutidas no bundle em tempo de build. Não armazene segredos aqui.

| Variável | Descrição | Exemplo |
|---|---|---|
| `PUBLIC_SITE_URL` | URL canônica (canonical, OG, sitemap) | `https://dsplayground.com.br` |
| `PUBLIC_API_URL` | Endpoint do backend de auth e ingestão | `https://api.dsplayground.com.br` |
| `PUBLIC_DASHBOARD_URL` | URL base do dashboard autenticado | `https://app.dsplayground.com.br/cliente/metricas` |
| `PUBLIC_PUBLISHABLE_KEY` | Publishable key da landing (dogfood) | `pk_production_...` |
| `PUBLIC_DEBUG` | Logs do SDK no console | `false` |

Copie `.env.example` para `.env` e ajuste os valores para o ambiente local.

---

## Deploy

O deploy é automático via **Cloudflare Pages** a cada push em `main`.

```
git push → Cloudflare Pages build → astro build → dist/ → CDN global
```

Variáveis de build são configuradas no dashboard do Cloudflare Pages. A variável `NODE_AUTH_TOKEN` é necessária para instalar o SDK durante o build.

---

## Repositórios relacionados

| Repositório | Descrição |
|---|---|
| [DSPlayAnalytics/backend](https://github.com/DSPlayAnalytics/backend) | API Flask — auth, ingestão, billing |
| [DSPlayAnalytics/SDK](https://github.com/DSPlayAnalytics/SDK) | SDK de analytics para browsers |

---

## Licença

MIT © [DSPlay Analytics](https://dsplayground.com.br)
