# Steem Bluepaper

This repository contains the LaTeX source code for the Bluepaper. The instructions to clone the repository and build the PDF using pandoc are described below.

Currently the build instructions are for Ubuntu 16.04 or higher. There is also separate script, which will build the PDF using docker, and can be used on other operating systems. Users are welcome to try out the build in their local environments and submit a pull request to update the readme instructions if they are able to get it to successfully build natively on a different OS.

## Using docker

First build will take a while, because docker image will need to be build. Next builds should be much faster :)

```
git clone https://github.com/steemit/bluepaper && cd blupaper
./build.sh
```

Bluepaper.pdf should be created.

## Ubuntu 16.04 or higher

### Installation Instructions

Install packages
```bash
sudo apt-get update
sudo apt install texlive-xetex
sudo apt-get install pandoc
```

Clone repository
```bash
git clone https://github.com/steemit/bluepaper
```

### Build Instructions

Open the bluepaper directory
```bash
cd ~/bluepaper
```

Compile using pandoc
```bash
pandoc Bluepaper.md --latex-engine=xelatex -o Bluepaper.pdf
```

After building, the pdf file will be output to:
```bash
./Bluepaper.pdf
```

### Build Instructions for Non-English language

Create a new folder for special font X
```bash
mkdir -p /usr/share/fonts/myfonts
```

Copy the font X into the new folder and run commands in it.
Create an index of scalable font files for font X. A new file fonts.scale is created.
```bash
sudo mkfontscale
```

Create an index of X font files in a directory. A new file fonts.dir is created.
```bash
sudo mkfontdir
```

Build font information cache files
```bash
sudo fc-cache -fv
```

Restart and run fc-list, the new font should be added.

Add extra setting for XeTeXlinebreaklocale. Go to /usr/share/pandoc/data/templates and export the template
```bash
pandoc -D latex > template.latex
```

Add "\XeTeXlinebreaklocale "zh" after below command.
```bash
$if(mathfont)$
    \setmathfont(Digits,Latin,Greek){$mathfont$}
$endif$
```

Complie using pandoc
```bash
pandoc -f markdown -t latex  -M mainfont:KaiTi_GB2312 --latex-engine=xelatex -o Bluepaper_CN.pdf --template=./template.latex Bluepaper_CN.md
```


