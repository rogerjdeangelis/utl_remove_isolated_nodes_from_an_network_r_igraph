# utl_remove_isolated_nodes_from_an_network_r_igraph
Remove isolated nodes from an network igraph wps proc r.  Keywords: sas sql join merge big data analytics macros oracle teradata mysql sas communities stackoverflow statistics artificial inteligence AI Python R Java Javascript WPS Matlab SPSS Scala Perl C C# Excel MS Access JSON graphics maps NLP natural language processing machine learning igraph DOSUBL DOW loop stackoverflow SAS community.


    Remove isolated nodes from an network igraph wps proc r

    WPS Proc R

    Before graphic
    https://tinyurl.com/yblks6xt
    https://github.com/rogerjdeangelis/utl_remove_isolated_nodes_from_an_network_r_igraph/blob/master/utl_remove_isolated_nodes_from_an_network_r_igraph_1.png

    After graphic
    https://tinyurl.com/ych7ywvf
    https://github.com/rogerjdeangelis/utl_remove_isolated_nodes_from_an_network_r_igraph/blob/master/utl_remove_isolated_nodes_from_an_network_r_igraph_2.png

    see github
    https://tinyurl.com/yambdfwc
    https://github.com/rogerjdeangelis/utl_remove_isolated_nodes_from_an_network_r_igraph

    StackOverflow
    https://tinyurl.com/ybny9y6w
    https://stackoverflow.com/questions/51271730/how-to-remove-small-communities-using-igraph-in-r

    GFW profile
    https://stackoverflow.com/users/4752675/g5w



    INPUT (directed graph)
    ======================

    SD1.HAVE total obs=11

     Obs    FRO    TOO

       1     1      2           2
       2     2      3          / \     disconneected
       3     3      1         /   \    community
                             1-----3

       4     a      b           a
       5     b      c          / \
       6     c      d         b   c
       7     d      a          \ /
                                d
                                |  connected communities
                                 f
       8     f      g            \
       9     g      h             g
      10     h      d              \
                                    h

                               ---
      11     9      9          |9|  isolated single community
                               ---

     +
     |                 c
     +                / \      f
     |               /   \      \
     +              /     \      g
     |             /       \      \
     +            a        d-------h
     |             \      /
     +              \    /
     |        ---    \  /
     +        |9|      b
     |     2  ---
     +    / \
     |   /   \
     +  1-----3
     |
     ---+---+---+---+---+---+---+---+--


    EXAMPLE OUTPUT  ( Remove the singleton 9 community)
    ---------------------------------------------------


     +
     |                 c
     +                / \      f
     |               /   \      \
     +              /     \      g
     |             /       \      \
     +            a        d-------h
     |             \      /
     + Isolated     \    /
     | community     \  /
     + removed         b
     |     2
     +    / \
     |   /   \
     +  1-----3
     |
     ---+---+---+---+---+---+---+---+--


    PROCESS
    =======

    %utlfkil(d:/png/utl_remove_isolated_nodes_from_an_network_r_igraph.png);
    %utl_submit_wps64('
    libname sd1 "d:/sd1";
    options set=R_HOME "C:/Program Files/R/R-3.3.2";
    libname wrk  sas7bdat "%sysfunc(pathname(work))";
    libname hlp  sas7bdat "C:\Progra~1\SASHome\SASFoundation\9.4\core\sashelp";
    proc r;
    submit;
    source("C:/Program Files/R/R-3.3.2/etc/Rprofile.site", echo=T);
    library(haven);
    library(igraph);
    have<-as.matrix(read_sas("d:/sd1/have.sas7bdat"));
    names<-have[,1];
    gD=graph.edgelist(have,directed=FALSE);
    lou <- cluster_louvain(gD);
    LO = layout_with_fr(gD);
    png("d:/png/utl_remove_isolated_nodes_from_an_network_r_igraph_1.png");
    plot(lou, gD, vertex.label = names , vertex.size=15,edge.arrow.size = .2, layout=LO);
    dev.off();
    Small = which(table(lou$membership) < 2);
    Keep = V(gD)[!(lou$membership %in% Small)];
    gD2  = induced_subgraph(gD, Keep);
    lou2 = cluster_louvain(gD2);
    LO2 = LO[Keep,];
    png("d:/png/utl_remove_isolated_nodes_from_an_network_r_igraph_2.png");
    plot(lou2, gD2, vertex.label = NA, vertex.size=15,edge.arrow.size = .2, layout=LO2);
    dev.off();
    endsubmit;
    run;quit;
    ');

    OUTPUT
    =====

    Before graphic
    https://tinyurl.com/yblks6xt

    After graphic
    https://tinyurl.com/ych7ywvf

     +
     |                 c
     +                / \      f
     |               /   \      \
     +              /     \      g
     |             /       \      \
     +            a        d-------h
     |             \      /
     + Isolated     \    /
     | community     \  /
     + removed         b
     |     2
     +    / \
     |   /   \
     +  1-----3
     |
     ---+---+---+---+---+---+---+---+--


    *                _               _       _
     _ __ ___   __ _| | _____     __| | __ _| |_ __ _
    | '_ ` _ \ / _` | |/ / _ \   / _` |/ _` | __/ _` |
    | | | | | | (_| |   <  __/  | (_| | (_| | || (_| |
    |_| |_| |_|\__,_|_|\_\___|   \__,_|\__,_|\__\__,_|

    ;

    data sd1.have;
      fro='1';too='2';output;
      fro='2';too='3';output;
      fro='3';too='1';output;
      fro='a';too='b';output;
      fro='b';too='c';output;
      fro='c';too='d';output;
      fro='d';too='a';output;
      fro='9';too='9';output;
      fro='f';too='g';output;
      fro='g';too='h';output;
      fro='h';too='d';output;
    run;quit;

    *          _       _   _
     ___  ___ | |_   _| |_(_) ___  _ __
    / __|/ _ \| | | | | __| |/ _ \| '_ \
    \__ \ (_) | | |_| | |_| | (_) | | | |
    |___/\___/|_|\__,_|\__|_|\___/|_| |_|

    ;

    see process
