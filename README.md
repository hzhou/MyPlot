### MyPlot.pm

Currently a Perl PDF library. Eventually this will be a general plotting library with multiple output modules (pdf, eps, windows, ...), like gnuplot.

### MyDef::output_plot

Plot module for MyDef.

### eps

Perl EPS macros.

## Example

```
page: test, basic_frame, t.pdf
    $group origin (200, 300), 10pt, gray, u=100
        $(for:i in 0,1,2)
            $(for:j in 0,1,2)
                $draw ($(i)u, $(j)u)
    $line 2, black
    $draw (2u,2u)--(0,0)--(0,3u)--(3u,0)--(0,0)
```

```
$ mydef_page -mplot test.def && perl test.pl
PAGE: test
  --> [./test.pl]
   --> t.pdf

```
![9 dots](9dots.png)
