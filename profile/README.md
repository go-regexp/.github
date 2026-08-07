<p align="center"><img src="https://raw.githubusercontent.com/go-regexp/brand/main/social/go-regexp.png" alt="go-regexp" width="720"></p>

<h1 align="center">go-regexp</h1>
<p align="center">Pure-Go regular expressions with lookahead, lookbehind and backreferences — the constructs RE2 forbids.</p>
<p align="center">
  <a href="https://go-regexp.github.io/docs/"><img src="https://img.shields.io/badge/docs-mkdocs--material-991B1B?style=flat-square&logo=materialformkdocs&logoColor=white" alt="docs"></a>
  <img src="https://img.shields.io/badge/repos-1-B91C1C?style=flat-square" alt="repos">
  <img src="https://img.shields.io/badge/Go-1.26.4-00ADD8?style=flat-square&logo=go&logoColor=white" alt="Go">
  <img src="https://img.shields.io/badge/license-BSD--3--Clause-991B1B?style=flat-square" alt="license">
</p>

---

## What is this?

`go-regexp` is a pure-Go (**CGO=0**) regular-expression engine of the [Onigmo](https://github.com/k-takata/Onigmo) lineage — the regex library Ruby uses — with a public API shaped like the standard library's `regexp` package.

The standard library `regexp` is built on RE2, which guarantees linear-time matching by **forbidding** the constructs that require backtracking. `go-regexp` supports them:

- **Lookahead** `(?=…)` / `(?!…)` and **lookbehind** `(?<=…)` / `(?<!…)`
- **Backreferences** `\1`, `\k<name>`
- **Atomic groups** `(?>…)` and possessive quantifiers
- **Subexpression calls** `\g<name>`, `\g<0>` (recursive patterns)
- Ruby/Onigmo character properties, `\h`/`\H`, `\R`, named groups, and more

It runs the backtracking VM for those patterns and transparently falls back to a linear-time lazy-NFA/DFA accelerator for the RE2-compatible subset, so the common case stays fast while the extra features remain available. The package is named `onigmo` (not `regexp`), so it imports alongside the standard library without an alias.

```go
re := onigmo.MustCompile(`v\d+\.\d+\.\d+(?=["<])`)
got := re.FindAllString(`a v1.2.3" b v4.5.6< c v9.9.9 d`, -1)
// got == []string{"v1.2.3", "v4.5.6"}
```

Consumed by [`go-ruby-regexp/regexp`](https://github.com/go-ruby-regexp/regexp) (the Ruby binding) and [`go-pkgx/bk`](https://github.com/go-pkgx/bk) (pantry recipe version matching).

## Repositories (1)

| Module | Kind | What it is | API |
|---|---|---|:--:|
| [`engine`](https://github.com/go-regexp/engine) | core | Pure-Go Onigmo-lineage regex engine; stdlib-`regexp`-shaped API with lookaround & backrefs. CGO=0. | [ref](https://pkg.go.dev/github.com/go-regexp/engine) |

> This list reflects the repos that actually exist in the org.

## Links

- 📖 Docs — <https://go-regexp.github.io/docs/>
- 🌐 Site — <https://go-regexp.github.io/>
- 🎨 Brand assets — <https://github.com/go-regexp/brand>

---
<p align="center"><sub>Branding in <a href="https://github.com/go-regexp/brand">go-regexp/brand</a>.</sub></p>
