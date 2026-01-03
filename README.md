# TeX Content Publisher

Reusable LaTeX template system for technical publishing.

## Architecture Flow

```mermaid
flowchart TD
    subgraph CORE["tex-content-publisher (CORE)"]
        P[preamble.tex] --> D[defaults/]
        D --> DC[colors.tex]
        D --> DL[logos.tex]
        D --> DY[layout.tex]
        P --> CS[codestyles/]
        CS --> ST[ST.tex]
        CS --> CPP[cpp.tex]
        CS --> PY[python.tex]
    end

    subgraph CONTENT["Your Content Repository"]
        M[main.tex] -->|"\\input{}"| P
        M -->|"\\input{}"| CS
        CFG[config-*.tex] -.->|overrides| D
    end

    M --> PDF[Compiled PDF]
```

## How It Works

```mermaid
flowchart LR
    A[Your .tex file] -->|1. Load preamble| B[preamble.tex]
    B -->|2. Check for overrides| C{config-*.tex exists?}
    C -->|Yes| D[Load your custom config]
    C -->|No| E[Load defaults/]
    D --> F[Apply styles]
    E --> F
    F -->|3. Load codestyle| G[codestyles/*.tex]
    G --> H[Ready to compile]
```

## Usage

Add as submodule in your repo:

```bash
git submodule add https://github.com/your-user/tex-content-publisher .tex-publisher
```

In your `.tex` document:

```latex
\input{.tex-publisher/preamble}
\input{.tex-publisher/codestyles/cpp}  % or ST, python

\begin{document}
    % Your content here
\end{document}
```

## Structure

```
tex-content-publisher/
├── preamble.tex          # Main layout
├── defaults/
│   ├── colors.tex        # Default colors
│   ├── logos.tex         # Default logos
│   └── layout.tex        # Header/footer
└── codestyles/
    ├── ST.tex            # Structured Text
    ├── cpp.tex           # C++
    └── python.tex        # Python
```

## Customization (Override Defaults)

```mermaid
flowchart TD
    subgraph Override["How to Customize"]
        A[Create config file in YOUR repo] --> B{Which config?}
        B -->|Colors| C["config-colors.tex"]
        B -->|Logos| D["config-logos.tex"]
        B -->|Layout| E["config-layout.tex"]
        C --> F[Define your colors]
        D --> G[Define your logos]
        E --> H[Define header/footer]
    end
```

Create these files in your local folder to override defaults:

| Config File | Purpose | Overrides |
|-------------|---------|-----------|
| `config-colors.tex` | Custom colors | `defaults/colors.tex` |
| `config-logos.tex` | Your logos | `defaults/logos.tex` |
| `config-layout.tex` | Header/footer | `defaults/layout.tex` |

## Adding New Codestyles

```mermaid
flowchart LR
    A[Create new .tex file] --> B[codestyles/newlang.tex]
    B --> C[Define lstdefinelanguage]
    C --> D[Define lstset with colors]
    D --> E[Use in your document]
```

1. Create `codestyles/yourlang.tex`
2. Define the language syntax highlighting
3. Import with `\input{.tex-publisher/codestyles/yourlang}`

## Available Codestyles

| Language | File | Use Case |
|----------|------|----------|
| Structured Text | `codestyles/ST.tex` | IEC 61131-3, PLCs |
| C++ | `codestyles/cpp.tex` | OpenCV, STL |
| Python | `codestyles/python.tex` | ML, scripting |