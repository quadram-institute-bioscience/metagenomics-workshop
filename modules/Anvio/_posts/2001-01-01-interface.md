---
title: The interface
---

> This page is based on the official [interface tutorial](https://merenlab.org/tutorials/interactive-interface/) from Anvi'o.


## Prepare a directory

Create a new directory and navigate into it to download a simple matrix dataset for practice:

```bash
mkdir anvio-interface
cd anvio-interface

# Download example dataset
wget http://merenlab.org/tutorials/interactive-interface/files/data.txt
```

We can have a first look at the data:

```bash
less -S -x 20 data.txt

# or a quick preview (first 10 lines, first 6 columns)
head -n 10 data.txt | cut -f 1-6
```

## Launch the interface

Activate the `anvio-dev` conda environment:

```bash
conda activate anvio-dev
```

then launch the Anvi'o interactive interface with:

```bash
anvi-interactive --manual -d data.txt \
    -p profile.db \
    --title "Taxonomic profiles of 690 gut metagenomes" 
```

:question: What is "profile.db"? 

:question: Using `anvi-interactive --help`, can you find what `--manual` does?

This will open a new window in your web browser with the Anvi'o interactive interface.

You will see the panel with the controls, but to render the actual data you need to click on the "Render" button (green button on the top left).

![button]({{ site.baseurl}}/{% link img/draw.png %})

:mag: try to zoom and pan the view using your mouse or the controls on the left side of the interface.

:palette: try changing the colours of some layers

↖ try using the "Data" pane to inspect what the mouse is pointing at

## Where is the dendrogram?

Our matrix does not have a dendrogram, because we did not provide any hierarchical clustering information.

However, we can generate a dendrogram based on the data in the matrix. This can be done using the `anvi-matrix-to-newick` command, that will produce a tree in [Newick format](https://en.wikipedia.org/wiki/Newick_format).

```bash
anvi-matrix-to-newick data.txt \
                         -o tree.txt

less tree.txt
```

## Relaunch the interface with the tree

To use the tree we just generated, we need to relaunch the interface with the `-t` option:

```bash
anvi-interactive --manual -d data.txt \
    -p profile.db\
    --title "Taxonomic profiles of 690 gut metagenomes" \
    --tree tree.txt  
```

