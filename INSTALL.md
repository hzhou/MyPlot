## Step 1. Install MyDef

MyDef is a general meta-layer for programming.

1. download

        $ git clone https://github.com/hzhou/MyDef.git

2. set up environment variables

        PATH=$PATH:$HOME/bin
        LIBRARY_PATH=$HOME/lib
        PERL5LIB=$HOME/lib/perl5
        MYDEFLIB=$HOME/lib/MyDef
        MYDEFSRC=$HOME/MyDef
        export PATH PERL5LIB MYDEFLIB MYDEFSRC

        alias pmake="perl Makefile.PL INSTALL_BASE=$HOME"

        # change accordingly, to the minimum, change MYDEFSRC to where you downloaded the source.

3. install

        $ sh bootstrap.sh

## Step 2. Install output_plot

output_plot is a MyDef module.

1. download

        $ git clone https://github.com/hzhou/MyPlot.git

2. install

        $ mydef_make
        $ make
        $ cd MyDef-output_plot
        $ pmake
        $ make install

        $ cd ..
        $ mydef_make
        $ sh install_def.sh

## Step 3. Install MyPlot

MyPlot is a perl module (with pdf, METAFONT, TeX routines).

    $ cd myplot
    $ mydef_make
    $ make
    $ cd MyPlot
    $ pmake
    $ make install
    $ cd ..
    $ mydef_make

    # It takes so many steps just to bootstrap. When update, only make, make install is needed.





