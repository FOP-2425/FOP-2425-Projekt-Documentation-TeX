# FOP-2425-Projekt-Documentation-TeX

[![Build LaTeX document](https://github.com/FOP-2425/FOP-2425-Documentation-TeX/actions/workflows/build.yml/badge.svg)](https://github.com/FOP-2425/FOP-2425-Documentation-TeX/actions/workflows/build.yml)
[![check](https://github.com/FOP-2425/FOP-2425-Documentation-TeX/actions/workflows/check.yml/badge.svg)](https://github.com/FOP-2425/FOP-2425-Documentation-TeX/actions/workflows/check.yml)

Die $\LaTeX$-Vorlage für die Dokumentation des FOP-Projekts im Wintersemester 2024/2025. Bitte wie bei anderen Abgaben auch den Quellcode der eigenen Abgabe nicht vor der Deadline veröffentlichen. (privates Repository)

## Automatisches Setup (empfohlen)
### Lokal (Devcontainer)
- [Docker](https://www.docker.com/) installieren
- [VS-Code](https://code.visualstudio.com/) (oder die Open-Source Variante Code-OSS) und [Remote-Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)-Extension installieren
- Dieses Repository klonen
- In VS-Code öffnen
- .vscode/settings.default.json in .vscode/settings.json kopieren
- Auf die Meldung "Reopen in Container" klicken
- Falls die Meldung nicht angezeigt werden sollte, kann der Container auch über die Command Palette (F1) geöffnet werden: `Remote-Containers: Reopen in Container`
- Für dark-mode kompillierung die Environment Variable `DARK_MODE=1` unter der Einstellung `"latex-workshop.latex.tools"` hinzufügen
### Lokal (Docker)
- [Docker](https://www.docker.com/) installieren
- Dieses Repository klonen
- kompilieren z.B. mit `docker run --rm -v $(pwd):/workspace -w /workspace make -j $(nproc)`
### Online (Sharelatex der TU-Darmstadt)
Falls eine Latex-Installation nicht möglich ist, haben wir hier auch eine Sharelatex-Vorlage erstellt: [Sharelatex](https://sharelatex.tu-darmstadt.de/project/65c94521794fdbaf65f8a7e4)

Um diese zu nutzen:
- Einloggen auf [Sharelatex](https://sharelatex.tu-darmstadt.de/)
- Den Link zum Template öffnen
- Menu -> Copy Project
- Projektname eingeben und auf "Create" klicken
## Manuelle Installation (nicht empfohlen, aufwendig)
- Latex-Installation (z.B. MikTex oder TexLive)
- Installation der [TU-Template](https://github.com/tudace/tuda_latex_templates) und der verwendeten Plugins (inklusive Logo!)
- Installation der [AlgoTeX-Vorlage](https://github.com/TUDalgo/AlgoTeX#algotex---die-latex-vorlage-der-fop-und-aud)

## Konfiguration des Formatters
Um eine einheitliche Formatierung aller Übungsblätter zu gewährleisten, muss Latexindent installiert und entsprechend konfiguriert werden, um die mitgelieferte [`latexindent.yaml`](latexindent.yaml) zu verwenden.
Ein Aufruf von latexindent könnte z.B. so aussehen:
```sh
latexindent.pl -l -w myfile.tex
```
in `VS-Code` mit LaTeX-Workshop kann man die Folgende Konfiguration verwenden:

```json
"latex-workshop.latexindent.args": [
    "-c",
    "%DIR%/",
    "%TMPFILE%",
    "-l",
    // "-m", // -m can have undesired sideeffects
    "-y=defaultIndent: '%INDENT%'"
],
```

Alternativ kann die Datei `defaultSettings.yaml` mit der mitgelieferten [`latexindent.yaml`](latexindent.yaml) überschrieben werden. Den Speicherort der Default Settings findet man über:
```sh
latexindent -vv
```

## Kompilieren
### Automatisches Kompilieren mit Makefile
Unter Unix-basierten Systemen kann das Projekt mit dem Befehl
```sh
make -j
```
kompiliert werden Dabei werden automatisch sowohl die light als auch die dark Variante parallel kompiliert und sind im Ordner `build` zu finden.
### Manuelles Kompilieren - Empfehlungen
- Empfohlener Compiler: [`latexmk`](https://ctan.org/pkg/latexmk?lang=de) mit [`LuaLaTeX`](http://www.luatex.org/)
- Empfohlene LaTeX-Distribution: [`TeX-Live`](https://www.tug.org/texlive/)
- Auflistung der Empfohlenen LaTeX-Editoren:
    - [VS-Code](https://code.visualstudio.com/) (oder die Open-Source Variante Code-OSS) mit [LaTeX-Workshop](https://github.com/James-Yu/LaTeX-Workshop)-Extension
    - [Neovim](https://neovim.io/) mit [VimTeX](https://github.com/lervag/vimtex)-Plugin
    - [IntelliJ Idea](https://www.jetbrains.com/de-de/idea/) mit [TeXiFy IDEA](https://plugins.jetbrains.com/plugin/9473-texify-idea)-Plugin
    - [TeX-Studio](https://www.texstudio.org/)
- Hinweise für das Auswählen von PDF-Viewern:
    - Ein guter PDF-Viewer sollte synctex unterstützen, sodass man zwischen Quellcode und PDF hin- und her springen kann
