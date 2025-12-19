![Banner](/img/Banner.png)

---

# 📄 doc-conv

A professional, batteries-included CLI tool for converting Markdown documents to PDF, DOCX, HTML, and more using pandoc.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Shell](https://img.shields.io/badge/Shell-Bash-green.svg)](https://www.gnu.org/software/bash/)
[![Version](https://img.shields.io/badge/version-1.0.0-blue.svg)](https://github.com/liiam-dsouza/doc-conv/releases)

## ✨ Features

- 🎯 **Simple CLI interface** - Intuitive flags and options
- 📏 **Flexible margins** - Set individual or uniform margins
- 🎨 **Multiple output formats** - PDF, DOCX, HTML, EPUB, and more
- 🤖 **Auto-setup** - Installs dependencies on first run
- 🎨 **Colorized output** - Beautiful, readable terminal output
- 🔍 **Dry-run mode** - Preview conversions before running
- 📝 **Verbose mode** - Detailed output for debugging
- ⚡ **Batch processing** - Easy to use in loops
- 🛡️ **Safe by default** - Won't overwrite files without `-f`
- 🚀 **Zero configuration** - Works out of the box

## 🚀 Installation

### Option 1: Homebrew (Recommended for macOS/Linux)

The easiest way to install and keep doc-conv up to date:

```bash
# Install from custom tap
brew install liiam-dsouza/tap/doc-conv

# Run setup to install dependencies
doc-conv --setup
```

**Updating:**
```bash
brew upgrade doc-conv
```

**Uninstalling:**
```bash
brew uninstall doc-conv
```

---

### Option 2: One-Line Install Script (Universal)

Quick installation for any Unix-like system:

```bash
curl -fsSL https://raw.githubusercontent.com/liiam-dsouza/doc-conv/main/install.sh | bash
```

**For cautious users** (review before running):
```bash
# Download the installer
curl -fsSL https://raw.githubusercontent.com/liiam-dsouza/doc-conv/main/install.sh -o install.sh

# Review it
less install.sh

# Run it
bash install.sh

# Clean up
rm install.sh
```

**Custom installation directory:**
```bash
INSTALL_DIR=$HOME/.local/bin curl -fsSL https://raw.githubusercontent.com/liiam-dsouza/doc-conv/main/install.sh | bash
```

---

### Option 3: GitHub Releases (Manual)

Download the latest release directly:

```bash
# Download latest version
curl -L https://github.com/liiam-dsouza/doc-conv/releases/latest/download/doc-conv -o doc-conv

# Make executable
chmod +x doc-conv

# Move to PATH (choose one)
sudo mv doc-conv /usr/local/bin/              # System-wide
mv doc-conv ~/.local/bin/                     # User-only (add to PATH if needed)

# Verify installation
doc-conv --version
```

**Specific version:**
```bash
VERSION=1.0.0
curl -L https://github.com/liiam-dsouza/doc-conv/releases/download/v${VERSION}/doc-conv -o doc-conv
chmod +x doc-conv
sudo mv doc-conv /usr/local/bin/
```

---

### Option 4: From Source (Development)

For contributors or those who want the latest unreleased features:

```bash
# Clone the repository
git clone https://github.com/liiam-dsouza/doc-conv.git
cd doc-conv

# Make executable
chmod +x doc-conv

# Install (choose one)
sudo cp doc-conv /usr/local/bin/               # System-wide
cp doc-conv ~/.local/bin/                      # User-only

# Or create a symlink for development
ln -s $(pwd)/doc-conv /usr/local/bin/doc-conv

# Run setup
doc-conv --setup
```

---

## 🔧 Post-Installation Setup

After installation, run the setup wizard to install dependencies:

```bash
doc-conv --setup
```

This will check for and optionally install:
- **pandoc** - Document converter (required)
- **BasicTeX/LaTeX** - For PDF generation (optional but recommended)

**Dependencies are only installed with your permission!**

---

## 📖 Quick Start

### Basic Usage

```bash
# Convert Markdown to PDF
doc-conv input.md pdf

# Convert to Word
doc-conv input.md docx

# Convert to HTML
doc-conv input.md html
```

### With Custom Margins

```bash
# All margins the same
doc-conv -m 2cm input.md pdf

# Individual margins (top, right, bottom, left)
doc-conv -t 1.5in -r 1in -b 1.5in -l 1in input.md pdf
```

### Advanced Usage

```bash
# Custom output filename
doc-conv -o final-report.pdf input.md pdf

# Output to specific directory
doc-conv -d ./output input.md pdf

# Overwrite existing files
doc-conv -f input.md pdf

# Preview without converting (dry run)
doc-conv --dry-run input.md pdf

# Verbose output for debugging
doc-conv --verbose input.md pdf
```

---

## 📚 Examples

### Academic Paper

```bash
# Narrow margins for academic journals
doc-conv -m 0.75in thesis.md pdf
```

### Business Document

```bash
# Standard 1-inch margins
doc-conv -m 1in proposal.md pdf
```

### Web Article

```bash
# Convert to HTML
doc-conv article.md html
```

### E-book

```bash
# Convert to EPUB
doc-conv book.md epub
```

### Batch Processing

```bash
# Convert all Markdown files to PDF
for file in *.md; do
  doc-conv "$file" pdf
done

# Convert with custom margins to output directory
for file in *.md; do
  doc-conv -m 2cm -d ./pdfs "$file" pdf
done

# Convert only if PDF doesn't exist
for file in *.md; do
  [[ ! -f "${file%.md}.pdf" ]] && doc-conv "$file" pdf
done
```

### With Make

```makefile
# Makefile
%.pdf: %.md
	doc-conv -m 1in $< pdf

all: $(patsubst %.md,%.pdf,$(wildcard *.md))

clean:
	rm -f *.pdf

.PHONY: all clean
```

---

## 🎛️ Command-Line Options

### General Options

| Option | Description |
|--------|-------------|
| `-h, --help` | Show help message and exit |
| `-v, --version` | Show version information |
| `--setup` | Run setup/dependency installer |

### Margin Options

| Option | Description | Example |
|--------|-------------|---------|
| `-m, --margin SIZE` | Set all margins | `-m 2cm` |
| `-t, --top SIZE` | Set top margin | `-t 1.5in` |
| `-r, --right SIZE` | Set right margin | `-r 1in` |
| `-b, --bottom SIZE` | Set bottom margin | `-b 1.5in` |
| `-l, --left SIZE` | Set left margin | `-l 1in` |

**Supported units:** `in` (inches), `cm` (centimeters), `mm` (millimeters), `pt` (points)

**Default:** All margins default to `1in` if not specified

### Output Options

| Option | Description | Example |
|--------|-------------|---------|
| `-o, --output FILE` | Custom output filename | `-o report.pdf` |
| `-d, --dir DIR` | Output directory | `-d ./output` |
| `-f, --force` | Overwrite existing files | `-f` |

### Debug Options

| Option | Description |
|--------|-------------|
| `--dry-run` | Preview conversion without executing |
| `--verbose` | Show detailed output and pandoc messages |
| `--no-color` | Disable colored terminal output |

---

## 📦 Supported Formats

### Input Format

Optimized for **Markdown** (`.md`) files with full GitHub Flavored Markdown support.

### Output Formats

| Format | Extension | Description | Notes |
|--------|-----------|-------------|-------|
| 📕 PDF | `.pdf` | Portable Document Format | Requires LaTeX |
| 📘 DOCX | `.docx` | Microsoft Word | Full formatting support |
| 🌐 HTML | `.html` | Web page | Standalone or fragment |
| 📗 EPUB | `.epub` | E-book | Reflowable layout |
| 📄 LaTeX | `.tex` | LaTeX source | For further customization |
| 📋 RTF | `.rtf` | Rich Text Format | Cross-platform |
| 📙 ODT | `.odt` | OpenDocument Text | LibreOffice compatible |
| 📰 RST | `.rst` | reStructuredText | Documentation |
| 📑 ORG | `.org` | Emacs Org-mode | Plain text |

And [many more](https://pandoc.org/MANUAL.html#output-formats) supported by pandoc!

---

## 💡 Tips & Tricks

### Shell Aliases

Add these to your `~/.zshrc` or `~/.bashrc`:

```bash
# Quick PDF conversion with 2cm margins
alias md2pdf='doc-conv -m 2cm'

# Convert and open immediately (macOS)
md2pdf-open() {
    doc-conv "$1" pdf && open "${1%.md}.pdf"
}

# Convert and open immediately (Linux)
md2pdf-open() {
    doc-conv "$1" pdf && xdg-open "${1%.md}.pdf"
}

# Batch convert all MD files in current directory
alias md2pdf-all='for f in *.md; do doc-conv "$f" pdf; done'
```

### Git Pre-commit Hook

Automatically generate PDFs when committing:

```bash
#!/bin/bash
# .git/hooks/pre-commit

# Convert any modified .md files to PDF
for file in $(git diff --cached --name-only --diff-filter=ACM | grep '\.md$'); do
    if [ -f "$file" ]; then
        echo "Generating PDF for $file..."
        doc-conv "$file" pdf
        git add "${file%.md}.pdf"
    fi
done
```

### Watch for Changes

Auto-convert when files change:

```bash
# Install fswatch (macOS)
brew install fswatch

# Watch and auto-convert
fswatch -o *.md | xargs -n1 -I{} sh -c 'doc-conv $(ls *.md | head -1) pdf'

# Or use entr (cross-platform)
ls *.md | entr doc-conv /_ pdf
```

### Custom Pandoc Options

For advanced users who need custom pandoc options, you can modify the script or use pandoc directly with doc-conv's margin calculation:

```bash
# Get the geometry string from doc-conv dry run
doc-conv --dry-run -m 2cm input.md pdf

# Use it with pandoc directly
pandoc input.md -o output.pdf --pdf-engine=xelatex \
  -V geometry:"top=2cm,right=2cm,bottom=2cm,left=2cm" \
  --toc \
  --number-sections
```

---

## 🆙 Updating

### Homebrew

```bash
brew upgrade doc-conv
```

### Install Script

```bash
curl -fsSL https://raw.githubusercontent.com/liiam-dsouza/doc-conv/main/install.sh | bash
```

### Manual

```bash
# Remove old version
sudo rm /usr/local/bin/doc-conv

# Download and install new version
curl -L https://github.com/liiam-dsouza/doc-conv/releases/latest/download/doc-conv -o doc-conv
chmod +x doc-conv
sudo mv doc-conv /usr/local/bin/
```

### Check Current Version

```bash
doc-conv --version
```

---

## 🗑️ Uninstalling

### Homebrew

```bash
brew uninstall doc-conv
rm -rf ~/.config/doc-conv  # Remove config files
```

### Manual Installation

```bash
# Remove binary
sudo rm /usr/local/bin/doc-conv

# Remove config directory (optional)
rm -rf ~/.config/doc-conv

# If installed to ~/.local/bin
rm ~/.local/bin/doc-conv
```

---

## 🐛 Troubleshooting

### "pandoc not found"

**Solution:**
```bash
doc-conv --setup
```

Or install manually:
```bash
# macOS
brew install pandoc

# Ubuntu/Debian
sudo apt-get install pandoc

# Fedora
sudo dnf install pandoc
```

---

### "xelatex not found" (for PDF generation)

**Solution:**
```bash
doc-conv --setup
```

Or install manually:
```bash
# macOS
brew install --cask basictex

# Ubuntu/Debian
sudo apt-get install texlive-xetex texlive-fonts-recommended

# Fedora
sudo dnf install texlive-xetex texlive-collection-fontsrecommended
```

---

### PDF generation fails with LaTeX errors

**Solution:**
```bash
# Update LaTeX package manager
sudo tlmgr update --self

# Install recommended font packages
sudo tlmgr install collection-fontsrecommended

# Run with verbose output to see the error
doc-conv --verbose input.md pdf
```

---

### "Permission denied" when installing

**Solution:**
```bash
# Make sure the script is executable
chmod +x doc-conv

# If moving to /usr/local/bin, use sudo
sudo mv doc-conv /usr/local/bin/

# Or install to user directory (no sudo needed)
mkdir -p ~/.local/bin
mv doc-conv ~/.local/bin/
export PATH="$HOME/.local/bin:$PATH"  # Add to ~/.zshrc or ~/.bashrc
```

---

### "Command not found" after installation

**Solution:**

Check if install directory is in your PATH:
```bash
echo $PATH
```

If not, add it to your shell config (`~/.zshrc` or `~/.bashrc`):
```bash
# For /usr/local/bin (should already be in PATH)
export PATH="/usr/local/bin:$PATH"

# For ~/.local/bin
export PATH="$HOME/.local/bin:$PATH"

# Reload shell
source ~/.zshrc  # or source ~/.bashrc
```

---

### Output file already exists

**Solution:**
```bash
# Use --force flag to overwrite
doc-conv -f input.md pdf

# Or use --dry-run to check first
doc-conv --dry-run input.md pdf
```

---

### Colors not showing in terminal

**Solution:**
```bash
# Your terminal might not support colors
# Use --no-color flag
doc-conv --no-color input.md pdf

# Or set TERM environment variable
export TERM=xterm-256color
```

---

### Conversion produces unexpected output

**Solution:**
```bash
# Use verbose mode to see what's happening
doc-conv --verbose input.md pdf

# Check your Markdown syntax
# Try a simple test file first
echo "# Test\n\nHello world" > test.md
doc-conv test.md pdf
```

---

## 🔐 Security

### Verifying Installation

When using the one-line installer, you can verify the script before running:

```bash
# Download and inspect
curl -fsSL https://raw.githubusercontent.com/liiam-dsouza/doc-conv/main/install.sh -o install.sh

# Review the code
less install.sh

# Check the hash (compare with published hash in releases)
shasum -a 256 install.sh

# Run it
bash install.sh
```

---

## 🤝 Contributing

Contributions are welcome! Here's how you can help:

### Reporting Bugs

1. Check if the bug has already been reported in [Issues](https://github.com/liiam-dsouza/doc-conv/issues)
2. If not, create a new issue with:
   - Your OS and version
   - doc-conv version (`doc-conv --version`)
   - Steps to reproduce
   - Expected vs actual behavior

### Suggesting Features

Open an issue with the `enhancement` label and describe:
- The use case
- Expected behavior
- Why it would be useful

### Submitting Pull Requests

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Test thoroughly
5. Commit with clear messages (`git commit -m 'Add amazing feature'`)
6. Push to your fork (`git push origin feature/amazing-feature`)
7. Open a Pull Request

### Development Setup

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/doc-conv.git
cd doc-conv

# Make changes
chmod +x doc-conv

# Test locally
./doc-conv --help
./doc-conv test.md pdf
```

---

## 👤 Author

**Liam D'Souza**
- GitHub: [@liiam-dsouza](https://github.com/liiam-dsouza)
- Repository: [doc-conv](https://github.com/liiam-dsouza/doc-conv)

---

## 🙏 Acknowledgments

This tool wouldn't be possible without:

- [**pandoc**](https://pandoc.org/) by John MacFarlane - Universal document converter
- [**BasicTeX**](https://www.tug.org/mactex/morepackages.html) - Lightweight LaTeX distribution
- [**XeTeX**](http://xetex.sourceforge.net/) - Unicode-based TeX typesetting engine

---

## 📊 Project Stats

- **Version:** 1.0.0
- **License:** MIT
- **Language:** Bash
- **Dependencies:** pandoc, LaTeX (optional)
- **Platforms:** macOS, Linux, Unix-like systems

---

## ❓ FAQ

**Q: Can I convert files other than Markdown?**  
A: Currently optimized for Markdown, but pandoc supports many input formats. You can modify the script or use pandoc directly for other formats.

**Q: Do I need LaTeX for all conversions?**  
A: No, LaTeX is only required for PDF generation. DOCX, HTML, EPUB, etc. work without it.

**Q: Can I customize the PDF styling?**  
A: Yes! Use custom pandoc templates or modify the script to add more pandoc options. Check the pandoc documentation for details.

**Q: Does it work on Windows?**  
A: Not directly, but you can use WSL (Windows Subsystem for Linux).

**Q: How do I report security vulnerabilities?**  
A: Please email security concerns privately rather than opening public issues.

**Q: Can I use this in commercial projects?**  
A: Yes! The MIT license allows commercial use. No attribution required (but appreciated).

**Q: How do I get help?**  
A: Open an issue on GitHub or check existing issues for solutions.

---

## 🌟 Show Your Support

If you find doc-conv useful, please consider:

- ⭐ **Starring** the repository
- 🐦 **Sharing** with others who might find it useful
- 🐛 **Reporting bugs** to help improve the tool
- 💡 **Suggesting features** for future versions
- 🤝 **Contributing** code or documentation

Every bit of support helps make doc-conv better!

---

**Made with ❤️ by [Liam D'Souza](https://github.com/liiam-dsouza)**

*Last updated: 2025-11-06*
