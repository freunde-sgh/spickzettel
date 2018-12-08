# Spickzettel-Archiv

Tools for creating the archive of the [Spickzettel](http://freunde-sgh.de/spickzettel)

# Workflow

1. Remove paper bindings

1. Scan all pages of an issue using a [ScanSnap 500](https://www.fujitsu.com/us/products/computing/peripheral/scanners/scansnap/ix500) into a single file and save it as `scanned/spickzettel_$i.pdf`, where `$i` is the issue number.

1. Open the scanned file in in Preview.app and turn all pages upright.

1. Split double pages into single ones:

   ```sh
   $ scripts/split-pages < scanned/spickzettel_$i.pdf > split/spickzettel_$i.pdf
   ```

1. Re-order pages:

   ```sh
   $ scripts/reorder-pages < split/spickzettel_$i.pdf > done/spickzettel_$i.pdf
   ```

1. Double-check uprightness manually in Preview.app (some pages need to be turned again after splitting).

1. Keep center-fold as single page (or re-join if applicable).

1. Create thumbnail of cover page:

   ```sh
   $ scripts/thumbnail done/spickzettel_$i.pdf
   ```

# Release

When you are done with a number of issues, create a new release and attach the PDFs to it:

```sh
$ GITHUB_ACCESS_TOKEN=XY..Z scripts/release 25 26 27 --tag 1.0
```

Then, upload new PDFs to freunde-sgh.de and assign the category "Spickzettel", which makes it appear in the [index page](http://freunde-sgh.de/spickzettel).

# TODO

* Make `split-pages` fit in with the other tools by having it take file names instead of using STDIN / STDOUT
*
