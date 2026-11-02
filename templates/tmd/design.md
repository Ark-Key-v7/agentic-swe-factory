---
manifold_version: "TEMPLATE_VALUE_REQUIRED — semver; bump on any law change, e.g. 1.0.0"
last_verified: "TEMPLATE_VALUE_REQUIRED — SHA of the commit that last modified this file. NEVER a date."
precedence: 5
name: "TEMPLATE_VALUE_REQUIRED — project title"
description: "TEMPLATE_VALUE_REQUIRED — one-line tagline"
# --- Official DESIGN.md token schema (normative; Stitch/impeccable-compatible) ---
colors:
  background: "oklch(0.13 0.01 260)"      # base surface
  foreground: "oklch(0.95 0.005 260)"     # base text
  primary: "TEMPLATE_VALUE"               # primary action
  secondary: "TEMPLATE_VALUE"             # secondary action (omit if unused)
  muted: "TEMPLATE_VALUE"                 # de-emphasized text/surface
  destructive: "TEMPLATE_VALUE"
  border: "TEMPLATE_VALUE"
  ring: "TEMPLATE_VALUE"                  # focus ring, ≥3:1 contrast
typography:
  display: { fontFamily: "TEMPLATE_VALUE", fontWeight: 600 }
  body: { fontFamily: "TEMPLATE_VALUE", fontSize: "1rem", lineHeight: 1.5 }
  mono: { fontFamily: "TEMPLATE_VALUE" }
rounded:
  default: "0.5rem"                       # one default radius
  raised: "0.75rem"                       # one raised-surface radius
spacing:
  base: "0.25rem"                         # 4pt system; all spacing in multiples
components:
  button-primary:
    backgroundColor: "{colors.primary}"
    textColor: "{colors.background}"
    rounded: "{rounded.default}"
# --- ARK extension keys (ignored by spec validators; carried for agency law) ---
ark:
  mode: "persuade"                        # persuade | operate | read | experience
  genre: "editorial"                      # editorial | modern-minimal | atmospheric | playful
  icon_library: "lucide-svelte"
  ui_primitive_library: "shadcn-svelte"   # mirrors the gravity.md Stack Manifest
  tokens_artifact: "src/styles/tokens.css"  # mirror of these values; this file governs, drift reconciles via PR
  motion_engine: "gsap"                   # the single engine
---

# DESIGN.MD — THE VISUAL PROTOCOL

Precedence rank 5 of 5. Subordinate to all other manifold files; the
constitutional layer (TMD Specification v2.1, §0: precedence, conflict halt,
manifest header, monorepo inheritance, instruction-file boundary) applies
verbatim. Binds to the Stack Manifest's ui_primitive_library and
styling_system slots (gravity.md). On cross-file conflict: HALT the Task
Contract and escalate MANIFOLD_CONFLICT per §0.2.

**Inert-state law:** for projects with no UI surface (project_type: service |
library), declare "INERT — no presentation layer" here and keep the file.

**Design-platform boundary:** external design platforms (canvas tools,
studios, generators) are design-time PRODUCERS. Their exports are source
material; this file is the system of record.

**Authorship:** humans ratify through the manifold PR. The ratified design
agent (ark-agents head-of-web-design) may draft entries; drafts carry
`derived_from` and become law only on merge. Amendments append with dated
notes, never silent overwrites.

**Normative model:** the frontmatter tokens are the law — machine-checkable,
linter-validatable, the name every component references. Body sections are
context: they explain application, record decisions, and carry the Do's and
Don'ts. When prose and tokens disagree, the tokens win and the prose gets
fixed.

## Overview

Creative North Star: one named metaphor for the whole system ("TEMPLATE_VALUE
— e.g. The Editorial Sanctuary"). Two to three sentences of personality,
density, and aesthetic philosophy, starting from the North Star. Mode and
genre from the `ark` block get their rationale here: what visitor success
looks like on these surfaces and why this register serves it. Close with a
Key Characteristics bullet list.

## Colors

One sentence of palette character, then the roles. All color use references
the frontmatter tokens by name — raw hex, rgb(), hsl(), or palette literals
outside this file are forbidden. Theme variants (dark/light) resolve through
the theme system, never through conditional classes in components. Contrast
floors: 4.5:1 body text, 3:1 large text and essential UI.

## Typography

The three font roles from the frontmatter (display, body, mono — at most
three families; two is the norm). Components reference roles by token name
only; undeclared font-family values are forbidden. Scale rule (e.g. Tailwind
text-* steps or a named ratio), heading weights, and the measure target
(45–75 characters for running text).

## Layout

Declared page regions and per-breakpoint container padding. Mobile-first:
shifts only at the declared breakpoints; desktop-first design and custom
breakpoints are forbidden. Spacing in multiples of the 4pt base. Pages
compose declared regions; ad-hoc page-level markup soup is out.

## Elevation & Depth

The project's depth philosophy in one phrase (flat with tone steps /
ambient shadow / structural lift). Shadows and glows on resting elements
are the anti-pattern; tone steps between surfaces are the default. What
truly floats (menus, dialogs) may elevate.

## Shapes

The two radius tokens govern. Icons come from the single declared icon
library.

## Components

The primitive inventory from the declared ui_primitive_library: list each
permitted primitive and its composition rules (e.g. "Button: variants
primary|ghost|danger; icon+label; icon-only forbidden outside toolbars").
Components reference tokens via `{...}` refs. Every interactive primitive
defines its full state set through variant naming (e.g. `button-primary`,
`button-primary-hover`, `button-primary-focus`, `-active`, `-disabled`,
`-loading`): hover, focus-visible (ring token, keyboard reachable),
disabled, loading at minimum. Custom focus/hover overrides are forbidden.
Loading states use skeleton primitives, not spinners. Every destructive
action uses a confirmation dialog, never a bare destructive button. Empty
states render a defined block, never blank space.

## Motion

The single declared engine (`ark.motion_engine`); a second animation engine
in the dependency tree requires a PR here. Easing and durations come from
the declared motion tokens; browser-default easing on interactive elements
is forbidden. Animation touches transform and opacity only. Scroll-triggered
instances under 20 per page; groups of 10+ batch. `prefers-reduced-motion:
reduce` collapses spatial motion to an opacity crossfade ≤150ms; content
never depends on script or motion to appear. Scroll-jacking and
interaction-blocking animation are forbidden outright. Smooth-scroll layer
(Lenis) defaults ON for persuade/experience surfaces, OFF for operate/read,
always OFF under reduced-motion.

## Imagery & Visual Direction

Direction (real photography of the subject's world, illustration language,
or generated fills — with the honest-imagery rules that govern each).
Treatment: crop ratios, corners, filters. Exemplars with credits.
Backgrounds: flat fields or real photography; one field change per section.
Texture and elevation notes if used.

## Surface Briefs

One entry per public-facing surface, appended as the project grows:
surface, mode, conversion goal, section jobs, proof plan (by proof type),
`derived_from`, `last_reconciled`.

## Decisions & Provenance

PRD-approved design decisions, each with `derived_from` (source artifact or
external canon — vendor MCP, governing skill, or official docs, never
operator assumption) and `last_reconciled`. When an upstream source changes,
grep `derived_from` to enumerate entries needing reconciliation; that is a
governed PR, never a silent edit.

## Do's and Don'ts

**Do** reference every color, font, radius, and spacing step by token name.
**Do** compose primitives into domain components; never edit a primitive.
**Do** ship all interaction states via variant conventions.
**Do** respect the locked system across every page (diversification is
inverted on system-managed projects: pages share the system).
**Don't** use inline styles, `<style>` blocks, or raw values outside this
file's definitions.
**Don't** add components, icons, fonts, or engines outside the declared
inventories — that requires a PR here first.
**Don't** resolve themes with conditional classes; the theme owns variants.
**Don't** fabricate proof, metrics, testimonials, or imagery.

## Enforcement

Frontmatter tokens and `{...}` refs: token lint + Stitch/impeccable
validation at Stage 1. Component states and forbidden imports: component
rules + shadcn-ui lint. Visual outcomes: Stage-3 rendered verification
against the ephemeral preview. Anything ungated here is `enforcement:
manual-review` and is reviewed at the human gate — never silently
unenforced. Protocol: every change is a PR with the empirical reason in the
body, `manifold_version` bumped, `last_verified` advanced on merge; a PR
that fails to advance the headers is invalid.
