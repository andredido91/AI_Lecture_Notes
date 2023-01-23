# Notes of Artificial Intelligence
In this repository you can find the notes of the course of Artificial Intelligence held by A. Drago at Unife.

For a good compiling by starting from the very beginning (i.e. with just you `.tex` source, without other auxiliary files), compile the `.tex` source by running the following engines exactly in the order they are shown:
* (`pdfLaTeX` + `shell-escape`)
* `pdfLaTeX`
* `biber`
* `pdfLaTeX`
* `pdfLaTeX`

In the following they are explained one by one.

## `pdfLaTeX` + `shell-escape`
Within the text there are some (actually only 2) `tikz` plots that are very heavy to compile; if you also add all the other `tikz` plots, images, tables, etc., in the *same* compilation, these weigths are summed up and you can get a run out-of-memory error. There are three solutions to this problem:
1. reduce the resolution of the plots;
2. modify the memory limits by directly acting on the files in the `texmf` (installation) tree;
3. separately compile the "problematic" plots alone, in such a way to produce standalone images, and insert them in the following compilation as `.pdf` images. This will ensure you that the memory consumption of heavy plots is not summed to the other, thus lightening the memory.

In this file I'm using option (3). To achieve this, first put the command `\tikzexternalize`, from `tikz` libray `pgfplots.external` in the preamble. `\tikzexternalize` automatically externalizes every `tikzpicture` environment; so I momentarily disable it in the preamble (`\tikzexternaldisable`). Then, just put `\tikzexternalenable` and `\tikzexternaldisable` just before and after every picture you want to externalize with this method. Once you have done so, run the main file with **`pdfLaTeX` with `shell-escape` option**. Notice that it is enough to run in whis way only the lines with the pictures you want to externalize, so in this phase you should momentarily comment all the rest (otherwise from the point of view of memory nothing would change). This can take a while, and when is finished you will get a group of files for each externalized image (I put these in a separate folder, to keep some order). From this moment on, when you run your main `.tex` as you always would (i.e. with the normal `pdfLaTeX` compiler), the machine will automatically insert the externalized pictures as normal images. In summary, use `pdfLaTeX` + `shell-escape` only once in order to create the pictures (and any time you want to update them); once these files have been obtained, it will be enough as always to compile with the usual `pdfLaTeX`. Hence, if you already have at disposal these files (e.g., by downloading the folder TikzExternalize from this repository), just skip this step. To compile with the `shell-escape` option type the following in your command prompt:
> pdflatex -shell-escape Artificial_Intelligence.tex

## `pdfLaTeX`
The standard compilation to produce the `.pdf`.
## `biber`
To let LaTeX learn which is the bibliography.
## `pdfLaTeX` x2
To complete the compilation with references, bibliography and table of contents.
