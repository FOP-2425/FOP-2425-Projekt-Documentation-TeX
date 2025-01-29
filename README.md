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
- Auf die Meldung "Reopen in Container" klicken
- Falls die Meldung nicht angezeigt werden sollte, kann der Container auch über die Command Palette (F1) geöffnet werden: `Remote-Containers: Reopen in Container`
- Für dark-mode kompillierung die Environment Variable `DARK_MODE=1` unter der Einstellung `"latex-workshop.latex.tools"` hinzufügen
### Lokal (Docker)
- [Docker](https://www.docker.com/) installieren
- Dieses Repository klonen
- kompilieren z.B. mit `docker run --rm -v $(pwd):/workspace -w /workspace make -j $(nproc)`
### Online (Sharelatex der TU-Darmstadt)
Falls eine Latex-Installation nicht möglich ist, haben wir hier auch eine Sharelatex-Vorlage erstellt: [Sharelatex](https://sharelatex.tu-darmstadt.de/read/jgpctcmpxrby#d8d8f5)

Um diese zu nutzen:
- Einloggen auf [Sharelatex](https://sharelatex.tu-darmstadt.de/)
- Den Link zum Template öffnen
- Menu -> Copy Project
- Projektname eingeben und auf "Create" klicken
## Manuelle Installation (nicht empfohlen, aufwendig)
- Latex-Installation (z.B. MikTex oder TexLive)
- Installation der [TU-Template](https://github.com/tudace/tuda_latex_templates) und der verwendeten Plugins (inklusive Logo!)
- Installation der [AlgoTeX-Vorlage](https://github.com/TUDalgo/AlgoTeX#algotex---die-latex-vorlage-der-fop-und-aud)

## Formatieren
### Automatisch mit pre-commit hook
Der Pre-commit Hook formatiert die Dateien automatisch, bevor sie committet werden. Dieser Hook wird auch für die CI verwendet, um sicherzustellen, dass die Dateien immer formatiert sind.

um dem Pre-commit Hook zu verwenden, muss das python package `pre-commit` installiert werden. (siehe [Anleitung von Pre-commit](https://pre-commit.com/#install))
```sh
pip install pre-commit
```

> Hinweis: Auf manchen Linux-Distributionen, die python-Pakete nicht über pip installieren, sollte das Paket `pre-commit` bzw. `python3-pre-commit` über den Paketmanager installiert werden.

Dann kann der Pre-commit Hook mit folgendem Befehl installiert werden:
```sh
pre-commit install
```
Der Pre-commit Hook wird nun bei jedem Commit ausgeführt und formatiert die Dateien automatisch.

Falls der Pre-commit Hook unabhängig von einem Commit ausgeführt werden soll, kann er mit folgendem Befehl manuell ausgeführt werden:
```sh
pre-commit run -a
```

### Manuell mit latexindent
> Hinweis: Wenn VS-Code verwendet wird (mit oder ohne devcontainer), sollten die korrekten Einstellungen automatisch geladen werden.

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
    "-l=%WORKSPACE_FOLDER%/latexindent.yaml",
    // "-m", // -m can have undesired sideeffects
    "-y=defaultIndent: '%INDENT%'"
],
```

Alternativ kann die Datei `defaultSettings.yaml` mit der mitgelieferten [`latexindent.yaml`](latexindent.yaml) überschrieben werden. Den Speicherort der Default Settings findet man über:
```sh
latexindent -vv
```

## Kompilieren
### Automatisch mit IDE (empfohlen)
Die meisten LaTeX-Editoren bieten eine Möglichkeit, das Dokument automatisch zu kompilieren. In VS-Code kann dies z.B. mit der LaTeX-Workshop-Extension erreicht werden.
### Automatisch mit make
Das Übungsblatt kann IDE-Unabhängig mit dem Befehl `make -j` kompiliert werden. Der Parameter `-j` sorgt dafür, dass die Datei parallel kompiliert wird, was die Kompilierzeit verkürzt. Dabei werdeen die folgenden Versionen erstellt:
- light mode
- dark mode
- light mode ohne sichtbare Punktzahlen (für Reviewer)
- dark mode ohne sichtbare Punktzahlen (für Reviewer)
### Automatisch mit act
Falls **genau** die gleiche Umgebung wie in der CI benötigt wird, kann `act` verwendet werden. Act nutzt Docker, um die CI-Umgebung lokal zu simulieren. Dann kann der Build mit folgendem Befehl ausgeführt werden:
```sh
act -j build --artifact-server-path /tmp/artifacts
```
Die erstellten PDFs werden dann im Ordner `/tmp/artifacts` abgelegt. (bei Bedarf kann der Pfad angepasst werden)

## Spell checking
Für Spell checking mit VS-Code empfehlen wir LTex, eine entsprehcende Konfiguration ist vorgegeben.

LTex ist standardmäßig auf Deutsch eingestellt. Wenn ein englischer Abschnitt geprüft werden soll, kann die Sprache dafür temporär auf Englisch gestellt werden:
```latex
% Deutscher Text
Das ist ein Test
\begin{otherlanguage}{english}
    % Englischer Text
    This is a test.
\end{otherlanguage}
```

## Empfehlungen für LaTeX-Distribution und -Editoren
- Empfohlener Compiler: [`latexmk`](https://ctan.org/pkg/latexmk?lang=de) mit [`LuaLaTeX`](http://www.luatex.org/)
- Empfohlene LaTeX-Distribution: [`TeX-Live`](https://www.tug.org/texlive/)
- Auflistung der Empfohlenen LaTeX-Editoren:
    - [VS-Code](https://code.visualstudio.com/) (oder die Open-Source Variante Code-OSS) mit [LaTeX-Workshop](https://github.com/James-Yu/LaTeX-Workshop)-Extension
    - [Neovim](https://neovim.io/) mit [VimTeX](https://github.com/lervag/vimtex)-Plugin
    - [IntelliJ Idea](https://www.jetbrains.com/de-de/idea/) mit [TeXiFy IDEA](https://plugins.jetbrains.com/plugin/9473-texify-idea)-Plugin
    - [TeX-Studio](https://www.texstudio.org/)
- Hinweise für das Auswählen von PDF-Viewern:
    - Ein guter PDF-Viewer sollte synctex unterstützen, sodass man zwischen Quellcode und PDF hin- und her springen kann
