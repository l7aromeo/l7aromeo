<div align="center">

# Ukasyah Rahmatullah Zada

[![Role](https://img.shields.io/badge/Role-Software%20Engineer-blue?style=flat-square)](https://ukasyah.meoverse.com)
[![Core](https://img.shields.io/badge/Core-Rust-CE422B?style=flat-square&logo=rust&logoColor=white)](https://github.com/l7aromeo?tab=repositories&language=rust)
[![Surface](https://img.shields.io/badge/Surface-TypeScript-3178C6?style=flat-square&logo=typescript&logoColor=white)](https://www.npmjs.com/~l7aromeo)
[![Status](https://img.shields.io/badge/Status-Streaming%20coffee%20over%20TCP-brown?style=flat-square&logo=coffeescript&logoColor=white)](https://github.com/l7aromeo)
[![Location](https://img.shields.io/badge/Location-Jakarta%2C%20ID-58a6ff?style=flat-square&logo=googlemaps&logoColor=white)](https://ukasyah.meoverse.com)
[![Portfolio](https://img.shields.io/badge/Portfolio-ukasyah.meoverse.com-2FCBA8?style=flat-square&logo=firefoxbrowser&logoColor=white)](https://ukasyah.meoverse.com)
[![Sponsor](https://img.shields.io/badge/Sponsor-Me-ff5f5f?style=flat-square&logo=ko-fi&logoColor=white)](https://ko-fi.com/l7aromeo)

<div align="left">

```typescript
const developer = {
  role: "Senior Software Engineer @ PT Media Info Grup Indonesia",
  builds: ["Frameworks", "Compilers", "Layout", "Rendering"],
  core: "Rust",
  surface: ["TypeScript", "JavaScript"],
  motto: "What you describe, lowered until it is pixels.",
  status: "Streaming coffee over TCP (Totally Coffee Protocol)"
};
```

</div>

I build the layer underneath. A description becomes source, source becomes a
compiled call, a call becomes elements, elements become solved boxes, and boxes
become pixels. I have shipped something at every one of those levels.

JavaScript was the arena. Rust is the core now, with TypeScript on the outside
where it belongs, as the part you hold.

</div>

---

## The stack, as owned

Six published packages, grouped by line and ordered by depth within it. The
further down one goes, the more of it is Rust; TypeScript stays at the surface,
as the API you touch. Five are mine from scratch, and the rasteriser at the
bottom started as someone else's and says so.

The depths are a taxonomy, not a pipeline. `@meonode/ui`, `@meonode/mui` and
`@meonode/compiler` are one line, ending where React takes over. `meo-canvas`
and `meo-skia-canvas` are another, generating images server-side with no React
in them. `meocord` is neither. The two lines share the shape of the work and no
code.

<table>
<tr>
<td width="20%" align="center"><strong>00 · source</strong><br/><sub>TypeScript</sub></td>
<td>

### [@meonode/ui](https://ui.meonode.com): React without JSX

Type-safe React components with no JSX and no build step: plain functions
replace it, with no transform and no syntax extension. CSS properties as props,
theme paths through React context, opt-in per-node memoization, and full Server
Components support.

```typescript
Div({ padding: 24, children: H1('Hello World') })
```

[![npm](https://img.shields.io/npm/v/@meonode/ui?style=flat-square&logo=npm)](https://www.npmjs.com/package/@meonode/ui)
[![downloads](https://img.shields.io/npm/dm/@meonode/ui?style=flat-square&color=58a6ff)](https://www.npmjs.com/package/@meonode/ui)

</td>
</tr>
<tr>
<td align="center"><strong>00 · source</strong><br/><sub>TypeScript</sub></td>
<td>

### [@meonode/mui](https://www.npmjs.com/package/@meonode/mui): MUI, composed as nodes

A lightweight wrapper putting `@mui/material` components behind MeoNode
factories, so an MUI tree composes the way the rest of a `@meonode/ui` page
does. Fully typed, tree-shakeable, no abstraction overhead at runtime. Peer
dependencies only: it ships no MUI, no Emotion and no second copy of React.

[![npm](https://img.shields.io/npm/v/@meonode/mui?style=flat-square&logo=npm)](https://www.npmjs.com/package/@meonode/mui)

</td>
</tr>
<tr>
<td align="center"><strong>01 · compile</strong><br/><sub>Rust → WASM</sub></td>
<td>

### [@meonode/compiler](https://www.npmjs.com/package/@meonode/compiler): the optional lowering step

An experimental SWC plugin in Rust, compiled to `wasm32-wasip1`, that rewrites
`@meonode/ui` call sites into pre-partitioned marker props at build time, so
the runtime skips prop classification and signature hashing on every render.

Optional on purpose: `@meonode/ui` needs no build step, and this is an
optimisation on top of one.

```rust
// call site in, marker props out, before the browser ever sees it
```

[![npm](https://img.shields.io/npm/v/@meonode/compiler?style=flat-square&logo=npm)](https://www.npmjs.com/package/@meonode/compiler)

</td>
</tr>
<tr>
<td align="center"><strong>00 · source</strong><br/><sub>Rust core</sub></td>
<td>

### [meo-canvas](https://l7aromeo.github.io/meo-canvas/): server-side image generation

A declarative scene description turned into a rendered image, laid out with CSS
flexbox, grid and block rules and drawn on Skia. Two surfaces, one renderer: a
Rust library crate and a Node addon over the same core. Layout, text shaping,
painting and encoding all happen in Rust. The Node surface describes a scene and
asks for pixels, and nothing is drawn in JavaScript. No React, and no
relationship to `@meonode/ui`.

Taffy solves the layout since v10, which is what brought grid and block
alongside flexbox.

```typescript
await Root({ children: Text('Generated server-side, no browser') })
```

[![npm](https://img.shields.io/npm/v/meo-canvas?style=flat-square&logo=npm)](https://www.npmjs.com/package/meo-canvas)

</td>
</tr>
<tr>
<td align="center"><strong>04 · raster</strong><br/><sub>Rust core</sub></td>
<td>

### [meo-skia-canvas](https://www.npmjs.com/package/meo-skia-canvas): the rasteriser

A Skia-backed HTML Canvas 2D API for Rust and Node: GPU-accelerated,
multi-threaded, with PDF and SVG vector export. Wide-gamut colour across eight
spaces through Rec. 2020, float compositing, and HDR transfer functions (PQ and
HLG) tagged into 10- and 12-bit AVIF. Prebuilt binaries ship as optional
platform packages.

Started as a fork of Christian Swinehart's excellent
[skia-canvas](https://github.com/samizdatco/skia-canvas), which targets Node.
This one adds a Rust crate beneath the addon, so the renderer can be *linked*
as well as required, which is how `meo-canvas`, itself a Rust crate, paints. It
also adds decode, encode, GPU and GUI modules.

[![npm](https://img.shields.io/npm/v/meo-skia-canvas?style=flat-square&logo=npm)](https://www.npmjs.com/package/meo-skia-canvas)

</td>
</tr>
<tr>
<td align="center"><strong>—</strong><br/><sub>TypeScript</sub></td>
<td>

### [meocord](https://www.npmjs.com/package/meocord): Discord bot framework for Node

Decorator-based framework on discord.js, bringing controllers, services, guards
and dependency injection to bot development, with a full CLI and testing
utilities out of the box.

```typescript
@Command()
class HelloCommand {}
```

[![npm](https://img.shields.io/npm/v/meocord?style=flat-square&logo=npm)](https://www.npmjs.com/package/meocord)

</td>
</tr>
</table>

### Built on it

[Chu Tao](https://chutao.meoverse.com) is a multi-service Discord bot across
four live-service games (Genshin Impact, Honkai: Star Rail, Zenless Zone Zero,
Neverness to Everness): a discord.js bot, a Rust REST API on axum and SeaORM,
and a Next.js portal for OAuth and account linking. Every card is rendered
in-process by `meo-canvas`: no browser in the image.

---

## Tools

<table align="center">
<tr>
<td width="50%" valign="top">

### Languages and core

```typescript
const languages = {
  core: "Rust",                            // what the work is made of
  surface: ["TypeScript", "JavaScript"],   // what you hold it by
  jvm: ["Kotlin", "Java"],
  also: ["PHP", "Python"]
};
```

### Frontend

```typescript
const frontend = [
  "React", "Next.js", "Remix",
  "Redux", "React Native",
  "@meonode/ui"
];
```

### Backend and APIs

```typescript
const backend = {
  frameworks: ["NestJS", "axum", "meocord", "Laravel", "Spring Boot"],
  data: ["SeaORM", "Prisma"],
  protocols: ["REST", "GraphQL", "OpenAPI"],
  messaging: ["RabbitMQ"],
  search: ["Elasticsearch"]
};
```

</td>
<td width="50%" valign="top">

### Graphics and compilers

```rust
// where most of the interesting work happens
let toolchain = ["Skia", "Taffy", "SWC", "WebAssembly", "Neon", "N-API"];
```

### Data

```sql
SELECT * FROM skills WHERE category = 'database';
-- PostgreSQL, MariaDB, MongoDB, Redis, Elasticsearch
```

### DevOps and infrastructure

```yaml
infrastructure:
  - Docker
  - GitLab Runner
  - CI/CD Pipelines
  - Microservices
  - Event-Driven Architecture
```

### Testing and tooling

```typescript
const tools = ["Vitest", "Jest", "Vite", "Postman", "Git", "Sentry"];
```

</td>
</tr>
</table>

---

## Support my work

<div align="center">

If you're getting use out of the MeoNode ecosystem or meocord, a coffee helps
sustain the infrastructure and the time these keep asking for.

[![Ko-fi](https://img.shields.io/badge/Buy%20me%20a%20coffee-ff5f5f?style=for-the-badge&logo=ko-fi&logoColor=white)](https://ko-fi.com/l7aromeo)

</div>

---

## Development stats

<div align="center">

<table>
<tr>
<td width="50%" align="center">

### GitHub analytics

<img src="https://github-profile-summary-cards.vercel.app/api/cards/stats?username=l7aromeo" alt="GitHub Stats" />

</td>
<td width="50%" align="center">

### Language distribution

<img src="https://github-profile-summary-cards.vercel.app/api/cards/most-commit-language?username=l7aromeo&layout=compact&hide_border=true&theme=tokyonight&bg_color=0d1117&title_color=58a6ff&text_color=c9d1d9&langs_count=8&hide=html,css" alt="Top Languages" />

</td>
</tr>
</table>

### Contribution streak

<img src="https://streak-stats.demolab.com/?user=l7aromeo&theme=tokyonight&hide_border=true&background=0d1117&ring=58a6ff&fire=58a6ff&currStreakLabel=58a6ff&sideLabels=c9d1d9&dates=8b949e" alt="GitHub Streak" width="100%" />

</div>

---

## Connect with me

<div align="center">

[![Portfolio](https://img.shields.io/badge/Portfolio-ukasyah.meoverse.com-2FCBA8?style=for-the-badge&logo=firefoxbrowser&logoColor=white)](https://ukasyah.meoverse.com)
[![Email](https://img.shields.io/badge/Email-ukasyahrz%40outlook.com-0078D4?style=for-the-badge&logo=microsoftoutlook&logoColor=white)](mailto:ukasyahrz@outlook.com)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-l7aromeo-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/l7aromeo)
[![Discord](https://img.shields.io/badge/Discord-l7aromeo-5865F2?style=for-the-badge&logo=discord&logoColor=white)](https://discord.com/users/704803255561224264)
[![npm](https://img.shields.io/badge/npm-l7aromeo-CB3837?style=for-the-badge&logo=npm&logoColor=white)](https://www.npmjs.com/~l7aromeo)
[![GitLab](https://img.shields.io/badge/GitLab-l7aromeo-FC6D26?style=for-the-badge&logo=gitlab&logoColor=white)](https://gitlab.com/l7aromeo)

---

*Open to collaboration.*

![Profile Views](https://komarev.com/ghpvc/?username=l7aromeo&color=58a6ff&style=flat-square&label=Profile+Views)

</div>
