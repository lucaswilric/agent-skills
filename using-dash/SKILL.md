---
name: using-dash
description: "Look up API docs, method signatures, CLI commands, and language references in Dash. Prefer over web search for detailed documentation lookups. Use when answering questions about APIs, classes, functions, CLI flags, or language features."
---

# Dash Documentation Lookup

Look up documentation locally via Dash instead of searching the web. Faster, cheaper, and works offline.

## When to Use

- Answering detailed questions about APIs, method signatures, or class interfaces
- Looking up CLI command flags and options (e.g. AWS CLI, Terraform)
- Checking language built-ins, stdlib modules, or framework APIs
- Any time you'd otherwise `web_search` for reference documentation

## When NOT to Use

- Searching for tutorials, blog posts, or conceptual explanations
- Looking up libraries/tools that aren't in the installed docsets
- When the user explicitly asks to search the web

## Installed Docsets

Check available docsets with `mcp__dash__list_installed_docsets`. The identifier is needed for search calls.

Current docsets and their identifiers:

| Docset | Identifier |
|---|---|
| Go | `whlzlbnf` |
| AWS CLI | `oiirhfmh` |
| Terraform | `kjqozdfb` |
| DuckDB (gem) | `drdmtbzb` |
| AWS CloudFormation | `jwqthogi` |
| Trino | `lsucyylv` |
| aws-sdk-go-v2/aws | `dbhtdphc` |
| DuckDB | `jushgeag` |
| Ruby | `xuutgugy` |
| Ruby on Rails | `tykxapwc` |
| Python | `yxkekryk` |
| Buildkite | `iizrquzn` |

**Note:** Identifiers change when docsets are updated. If searches return no results for a known docset, re-run `mcp__dash__list_installed_docsets` to refresh identifiers.

## Workflow

### 1. Search for documentation

```
mcp__dash__search_documentation(query="ActiveRecord::Base", docset_identifiers="tykxapwc")
```

- Use the identifier from the table above (or from `list_installed_docsets`)
- Search multiple docsets by comma-separating identifiers: `"whlzlbnf,yxkekryk"`
- Set `max_results` to limit results (default 100, max 1000)

### 2. Load a documentation page

Search results include a `load_url`. Use it to fetch the full page:

```
mcp__dash__load_documentation_page(load_url="<url from search result>")
```

### 3. Enable full-text search (if needed)

Some docsets have full-text search disabled by default. If keyword searches return poor results, enable it:

```
mcp__dash__enable_docset_fts(identifier="whlzlbnf")
```

This only needs to be done once per docset.

## Tips

- Search with class/module names for best results: `"http.Client"` not `"how to make http request in go"`
- If a search returns too many results, add the method name: `"http.Client.Do"`
- Load the page to get full details — search results only show titles and snippets
