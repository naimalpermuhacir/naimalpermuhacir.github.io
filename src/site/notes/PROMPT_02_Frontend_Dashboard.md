---
tags:
  - prompt
  - frontend
  - bugzora
aliases:
  - Frontend Prompt
parent: "[[09_UI_UX_Tasarimi]]"
dg-publish: true
---

# PROMPT 02 - BugZora Frontend Dashboard

> **📎 Referans Dosyalar** — Bu promptu kullanmadan önce aşağıdaki dokümanları bağlam olarak ekle:
> - `@09_UI_UX_Tasarimi.md` — Ekran listesi, kullanıcı akışları, design system, bileşenler
> - `@06_API_Tasarimi.md` — Tüm API endpoint'leri, request/response şemaları
> - `@08_SaaS_Modeli_Fiyatlandirma.md` — Plan/özellik matrisi, kısıtlamalar, upgrade akışları
> - `@03_Yazilim_Mimarisi.md` — Genel sistem mimarisi ve servis haritası

You are a senior frontend engineer specializing in Next.js 14, TypeScript, Tailwind CSS and design systems.
Build the BugZora SaaS dashboard for a multi-tenant DevSecOps platform.

## Required Stack
- Next.js 14 App Router
- TypeScript
- Tailwind CSS
- shadcn/ui
- TanStack Query
- TanStack Table
- Recharts or Visx
- NextAuth.js

## Product Requirements
- Dashboard overview
- Scan jobs list and detail
- Vulnerability detail page
- SBOM viewer and analytics
- Policy management
- Report builder
- Integrations settings
- Tenant settings
- User management
- Billing page
- Audit logs

## UX Requirements
- Fast navigation
- Excellent empty/loading/error states
- Dark mode
- WCAG 2.1 AA support
- Mobile responsive layouts

## Project Structure
```text
/app/(auth)
/app/(dashboard)
/components
/components/charts
/components/data-table
/components/forms
/lib/api
/lib/auth
/lib/utils
/hooks
/types
/mocks
```

## Authentication
- Use NextAuth.js.
- Support credentials flow and OAuth provider placeholders.
- Store tenant context safely.

## State and Data Fetching
- Use TanStack Query for server state.
- Keep UI state local or in lightweight stores.
- Add optimistic updates only where safe.

## Pages To Build
- /login
- /dashboard
- /scans
- /scans/[id]
- /vulnerabilities/[id]
- /sbom
- /policies
- /reports
- /integrations
- /settings/tenant
- /settings/users
- /billing
- /audit-logs

## Component Requirements
- KPI cards
- Trend charts
- Severity badges
- Filter bar
- Paginated data tables
- Side panels and drawers
- Confirmation dialogs
- Toast notifications

## Mock Data Requirements
- Generate realistic tenants, users, scan jobs, findings, policies, invoices and audit events.
- Make data internally consistent across pages.

## API Integration Requirements
- Create typed client wrappers.
- Centralize error normalization.
- Handle unauthorized and expired session flows.

## Acceptance Criteria
- The app should be runnable locally.
- Pages should be connected with realistic navigation.
- Charts and tables should render meaningful mock data.
- Design should feel like a real security SaaS product.

## Output Expectations
- Return full project code.
- Include setup steps.
- Include environment variables needed.
- Include reusable components and mock API adapters.
- Instruction 001: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 002: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 003: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 004: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 005: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 006: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 007: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 008: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 009: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 010: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 011: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 012: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 013: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 014: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 015: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 016: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 017: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 018: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 019: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 020: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 021: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 022: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 023: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 024: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 025: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 026: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 027: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 028: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 029: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 030: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 031: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 032: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 033: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 034: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 035: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 036: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 037: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 038: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 039: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 040: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 041: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 042: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 043: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 044: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 045: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 046: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 047: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 048: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 049: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 050: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 051: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 052: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 053: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 054: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 055: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 056: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 057: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 058: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 059: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 060: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 061: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 062: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 063: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 064: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 065: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 066: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 067: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 068: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 069: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 070: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 071: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 072: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 073: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 074: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 075: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 076: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 077: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 078: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 079: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 080: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 081: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 082: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 083: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 084: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 085: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 086: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 087: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 088: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 089: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 090: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 091: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 092: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 093: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 094: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 095: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 096: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 097: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 098: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 099: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 100: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 101: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 102: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 103: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 104: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 105: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 106: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 107: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 108: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 109: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 110: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 111: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 112: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 113: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 114: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 115: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 116: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 117: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 118: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 119: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 120: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 121: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 122: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 123: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 124: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 125: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 126: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 127: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 128: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 129: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 130: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 131: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 132: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 133: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 134: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 135: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 136: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 137: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 138: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 139: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 140: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 141: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 142: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 143: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 144: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 145: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 146: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 147: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 148: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 149: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 150: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 151: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 152: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 153: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 154: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 155: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 156: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 157: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 158: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 159: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 160: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 161: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 162: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 163: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 164: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 165: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 166: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 167: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 168: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 169: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 170: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 171: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 172: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 173: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 174: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 175: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 176: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 177: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 178: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 179: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 180: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 181: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 182: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 183: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 184: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 185: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 186: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 187: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 188: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 189: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 190: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 191: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 192: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 193: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 194: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 195: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 196: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 197: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 198: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 199: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 200: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 201: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 202: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 203: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 204: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 205: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 206: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 207: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 208: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 209: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 210: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 211: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 212: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 213: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 214: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 215: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 216: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 217: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 218: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 219: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 220: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 221: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 222: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 223: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 224: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 225: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 226: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 227: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 228: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 229: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 230: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 231: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 232: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 233: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 234: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 235: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 236: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 237: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 238: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 239: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 240: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 241: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 242: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 243: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 244: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 245: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 246: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 247: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 248: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 249: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 250: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 251: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 252: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 253: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 254: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 255: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 256: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 257: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 258: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 259: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 260: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 261: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 262: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 263: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 264: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 265: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 266: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 267: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 268: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 269: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 270: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 271: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 272: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 273: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 274: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 275: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 276: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 277: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 278: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 279: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.
- Instruction 280: prefer composable UI, typed props, accessible semantics, realistic states, and clean integration seams for later backend hookup.


---

## 🔗 İlgili Notlar

- [[09_UI_UX_Tasarimi]]
- [[06_API_Tasarimi]]
- [[03_Yazilim_Mimarisi]]
