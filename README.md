# TeX Content Publisher

Sistema de plantillas LaTeX reutilizable para publicación técnica.

## Uso

Agregar como submódulo en tu repo:

```bash
git submodule add https://github.com/tu-user/tex-content-publisher .tex-publisher
```

En tu documento `.tex`:

```latex
\input{.tex-publisher/preamble}
\input{.tex-publisher/codestyles/cpp}  % o ST, python

\begin{document}
    % Tu contenido aquí
\end{document}
```

## Estructura

```
tex-content-publisher/
├── preamble.tex          # Layout principal
├── defaults/
│   ├── colors.tex        # Colores default
│   ├── logos.tex         # Logos default
│   └── layout.tex        # Header/footer
└── codestyles/
    ├── ST.tex            # Structured Text
    ├── cpp.tex           # C++
    └── python.tex        # Python
```

## Override (Personalización)

Crea estos archivos en tu carpeta local para sobrescribir defaults:

- `config-colors.tex` → colores personalizados
- `config-logos.tex` → tus logos
- `config-layout.tex` → header/footer custom

## Codestyles Disponibles

| Lenguaje | Archivo | Uso |
|----------|---------|-----|
| Structured Text | `codestyles/ST.tex` | IEC 61131-3, PLCs |
| C++ | `codestyles/cpp.tex` | OpenCV, STL |
| Python | `codestyles/python.tex` | ML, scripting |