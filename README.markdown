# Spickzettel-Archiv

Tools for creating the archive of the [Spickzettel](http://freunde-sgh.de/spickzettel)

# Workflow

1. Remove paper bindings

1. Scan all pages of an issue using a [ScanSnap S1500](https://www.fujitsu.com/global/products/computing/peripheral/scanners/scansnap/discontinued/s1500/s1500.html) into a single file and save it as `scanned/spickzettel_$i.pdf`, where `$i` is the issue number.

1. Open the scanned file in in Preview.app and turn all pages upright.

1. Split double pages into single ones:

   ```sh
   $ scripts/split-pages scanned/spickzettel_$i.pdf split/spickzettel_$i.pdf
   ```

1. Re-order pages:

   ```sh
   $ scripts/reorder-pages split/spickzettel_$i.pdf done/spickzettel_$i.pdf 44 1 40 5 24 21 0 45 4 41 30 15 42 3 46 -1 6 39 38 7 8 37 14 31 32 13 18 27 26 19 20 25 16 29 12 33 34 22 23 10 35 36 9 28 17 2 43 11
   ```

   The arguments after the input and output file names must be the (real) page numbers as they appear in the input file. The reorder script will then use these arguments to move the pages into the correct order in the output document.

1. Double-check uprightness again manually in Preview.app (some pages need to be rotated again after splitting).

1. Optional: Keep center-fold as single page (or re-join if applicable).

1. Create thumbnail of cover page:

   ```sh
   $ scripts/thumbnail done/spickzettel_$i.pdf
   ```

# Release

When you are done with a number of issues, create a new release and attach the PDFs to it:

```sh
$ GITHUB_ACCESS_TOKEN=XY..Z scripts/release --tag 1.0 done/spickzettel_$i.pdf thumbnail/spickzettel_$i.png
```

Then, upload new PDFs to freunde-sgh.de and assign the category "Spickzettel", which makes it appear in the [index page](http://freunde-sgh.de/spickzettel).

# TODO

* Without full text, and not split yet:

  - spickzettel-34.pdf
  - spickzettel-36.pdf

* #37 has press marks and needs to have its [cropBox](https://pythonhosted.org/PyPDF2/PageObject.html#PyPDF2.pdf.PageObject.cropBox) set

* Document titles are mostly garbage, but may be useful for searching

* Many of the later issues do not have the cover page as #1, but the very last page. Need to split and move.
