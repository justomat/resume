# Resume

This repository contains the source code for Geraldi Sutanto's resume, built with [Typst](https://typst.app/).

## Prerequisites

To build the resume locally, you need to have Typst installed.

### Install Typst

**macOS (Homebrew):**
```bash
brew install typst
```

**Other platforms:**
Please refer to the [Typst installation guide](https://github.com/typst/typst#installation).

## Editing the Resume

The resume content is located in the `resume.typ` file. It uses the `basic-resume` package.

1.  Open `resume.typ` in your preferred text editor.
2.  Modify the content as needed. You can update your contact info, experience, projects, etc.
    *   **Note:** The resume uses a custom function `#generic-one-by-two(left: [...], right: [...])` for some sections like Certifications. Ensure you keep the named arguments `left:` and `right:`.

## Building the PDF

Once you have made your changes, you can compile the Typst file into a PDF.

Run the following command in your terminal:

```bash
typst compile resume.typ
```

This will generate (or overwrite) the `resume.pdf` file in the same directory.

## Contributing / Updating

1.  Make your changes to `resume.typ`.
2.  Compile the PDF to ensure it looks correct: `typst compile resume.typ`.
3.  Commit both `resume.typ` and `resume.pdf`.
4.  Push to the repository.
