* [ref] [MyDef](http://huizhou.gitbooks.io/programming-with-mydef/content/Installing.html)
* [ref] [curve](http://hz2.org/blog/hobby_curve.html)

### MyPlot.pm

Currently a Perl PDF library. Eventually this will be a general plotting library with multiple output modules (pdf, eps, windows, ...), like gnuplot.

### MyDef::output_plot

Plot module for MyDef.

### eps

Perl EPS macros.

## Example 1
[Showing some DSL syntax]
```
page: test, basic_frame, t.pdf
    #---- metafont type of algebra ----
    $set_point i=0:4, j=0:4, u=100
        zij=(i*u,j*u)
    #---- CSS type of styling ----
    $group origin (10, 300), 10pt, gray
        #---- standard MyDef macros ----
        $(for:i in 0,1,2)
            $(for:j in 0,1,2)
                $draw z$(i)$(j)
        #---- CSS like free style but imperative ----
        $line 2, black
        #---- metafont line syntax ----
        $draw z22--z00--z03--z30--z00

    $group origin (350, 320), 4pt, blue
        $draw z00..z01..z21..z20..z10..cycle
```

```
$ mydef_page -mplot test.def && perl test.pl
PAGE: test
  --> [./test.pl]
   --> t.pdf

```
![9 dots](docs/9dots.png)

Explore output_plot/tests/ for more.

## Example 2 (Sierpinsky)

Or symply Perl programming.
```
page: sierpinski, basic_frame, t.pdf
    my $str="A"
    my ($x, $y)=(10,10)
    my $step=10

    $for $i=0:4
        $call expand
        # $print $i: [$str]

    $line #2222ff
    $call plot
    MyPlot::stroke()

subcode: expand
    my $s_out=""
    &call each_char, $str
        $if $c eq 'A'
            $s_out.="B-A-B"
        $elif $c eq 'B'
            $s_out.="A+B+A"
        $else
            $s_out.=$c
    $str=$s_out

subcode: plot
    my @stack
    my $dir=0
    MyPlot::moveto($x,$y)
    &call each_char, $str
        $if $c eq 'A' or $c eq 'B'
            $call get_pos
            MyPlot::lineto($x,$y)
        $elif $c eq '+'
            $dir+=60
        $elif $c eq '-'
            $dir-=60

subcode: get_pos
    $x+=cos($dir*3.1415926535/180.0) *$step
    $y+=sin($dir*3.1415926535/180.0) *$step

#---------------------------------------- 
subcode: each_char(s)
    my $n=length($(s))
    $for $i=0:$n
        my $c=substr($(s), $i, 1)
        BLOCK
```

![sierpinski](docs/sierpinski.png)
