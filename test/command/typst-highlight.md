Highlighted text should be read as a `mark` span, round-tripping with
the Typst writer.

```
% pandoc -f typst -t native
#highlight[hello]
^D
[ Para [ Span ( "" , [ "mark" ] , [] ) [ Str "hello" ] ] ]
```

```
% pandoc -f markdown -t typst
[hello]{.mark}
^D
#highlight[hello]
```

```
% pandoc -f typst -t typst
#highlight[hello]
^D
#highlight[hello]
```

`highlight` may also wrap multiple paragraphs. A pandoc inline cannot
span paragraphs, so other inline-styling elements such as `emph` are
split at paragraph breaks and each paragraph is read with the styling
applied. `highlight` marks a whole region instead: a body with
paragraph breaks is read as a `mark` div, one highlighted region
spanning the paragraphs, which is also how Typst lays it out.

```
% pandoc -f typst -t native
Before.

#highlight[
  Para one.

  Para two.
]
^D
[ Para [ Str "Before." ]
, Div
    ( "" , [ "mark" ] , [] )
    [ Para [ Str "Para" , Space , Str "one." ]
    , Para [ Str "Para" , Space , Str "two." ]
    ]
]
```

```
% pandoc -f typst -t typst
Before.

#highlight[
  Para one.

  Para two.
]
^D
Before.

#block[
Para one.

Para two.

]
```

Highlight bodies may contain math, inline or display, without breaking
the reader.

```
% pandoc -f typst -t native
#highlight[$ a = b $]
^D
[ Para
    [ Span ( "" , [ "mark" ] , [] ) [ Math DisplayMath "a = b" ]
    ]
]
```

```
% pandoc -f typst -t native
#highlight[
  Para.

  $ c = d $
]
^D
[ Div
    ( "" , [ "mark" ] , [] )
    [ Para [ Str "Para." ] , Para [ Math DisplayMath "c = d" ] ]
]
```
