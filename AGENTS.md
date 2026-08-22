# AGENTS.md — SISTEPARD

Guía para agentes de IA trabajando en este repositorio.

## Stack (no negociable)

- Portal de producción: HTML5 + Tailwind CSS vía CDN + JavaScript vanilla. **Sin build step, sin React** (excepción: `frontend/`, migración Next.js en progreso).
- Backend: Supabase — PostgreSQL con RLS, Auth (PIN + Google OAuth), Storage privado, Edge Functions (Deno).
- Despliegue: GitHub Pages desde `main` → cada push a main es producción.
- Todo debe funcionar abriendo `.html` directo (file://).

## Reglas críticas

1. **NUNCA escribir credenciales en código.** Service keys y connection strings solo por variables de entorno (`SUPABASE_SERVICE_ROLE_KEY`, `SUPABASE_DB_CONN`). La anon key vive SOLO en `js/supabase_config.js`. Este repo ya filtró una contraseña de DB una vez — no repetirlo.
2. **Datos personales fuera del repo**: cédulas, fotos y padrones (`padron_*.json`) jamás se versionan.
3. **Encoding UTF-8 estricto.** No reescribir archivos completos con Get-Content/Set-Content de PowerShell 5.1 (corrompe acentos). Usar herramientas de edición o Node.js.
4. **Experimentación visual solo en `demo-*`**; módulos productivos se modifican tras aprobación explícita.
5. Validación estatutaria PRM es ley del dominio: género 40–60% (Art. 155), juventud ≥10% (Art. 154), militancia ≥3 años (Art. 151).

## Mapa rápido

| Ruta | Qué es |
|---|---|
| `*.html` (raíz) | Módulos productivos del portal |
| `js/` | Config central, auth, fotos |
| `supabase/functions/` | Edge Functions (auth server-side) |
| `admin/` | Aprovisionamiento de instancias |
| `clients/<id>/config.json` | Config multi-cliente (gitignored) |
| `estructura_db.sql` | Esquema semilla completo |

## Verificación mínima antes de commit

1. Extraer `<script>` inline de HTMLs modificados → `node --check` a cada uno.
2. `git status --short`: sin *.bak, test*.html, padron_*.json ni configs con secretos.
3. Sin marcadores residuales (PART2, BODY2, TODO-PENDIENTE).

Commits: conventional + descripción breve en español (feat:/fix:/security:/demo:).
