A citation with `form: none` produces no output, with or without
citeproc. With citeproc it still registers the reference and participates
in year-suffix disambiguation.

```
% pandoc -f typst -t plain
Before #cite(<doeAlpha>, form: none) after.
^D
Before after.
```

```
% pandoc -f typst -t plain --citeproc --bibliography command/typst-cite-none.bib
#cite(<doeAlpha>, form: none)

#cite(<doeBeta>)
^D
(Doe 2005b)

Doe, John. 2005a. Alpha. Test Press.

Doe, John. 2005b. Beta. Test Press.
```
