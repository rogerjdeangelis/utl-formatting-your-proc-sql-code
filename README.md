# utl-formatting-your-proc-sql-code
Formatting your proc sql code   
    %let pgm=utl-formatting-your-proc-sql-code;

    Formatting your proc sql code

    gitHub
    https://github.com/rogerjdeangelis/utl-formatting-your-proc-sql-code

    %let pgm=dna_030Lb; /* create sdtm lb * 030 is third in batch run of all programs */

    /*
     _                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    data sdtm_lb;
      set sashelp.class;
    run;quit;

    data sdtm_dm;
      set sashelp.classfit;
    run;quit;

    /*
     _ __  _ __ ___   ___ ___  ___ ___
    | `_ \| `__/ _ \ / __/ _ \/ __/ __|
    | |_) | | | (_) | (_|  __/\__ \__ \
    | .__/|_|  \___/ \___\___||___/___/
    |_|
    */

    proc sql noprint;
      select
         quote(strip(name))
        ,quote(strip(sex))
      into
         :_dnaNam separated by ","
        ,:_dnaSex separated by ","
      from
         sdtm_dm(obs=5);
    ;quit;

    /* _dnaNam="Alfred","Alice","Barbara","Carol","Henry" */
    /* _dnaSex="F","F","F","M","M"                         */

    proc sql;
      create
         table dna_030LbJynDm as
      select
         lb.*
        ,dm.lower
      from
         sdtm_lb as lb left join sdtm_dm as dm
      on
         dm.name = lb.name
      order
         by lb.name
    ;quit;
    /* I LIKE TO PLACE TIS AFTER EVERY CREATED SAS DATASET */
    /*-- Number of unique levels=19 for name from dna_030LbJynDm(obs=19) 23JUL2022:07:00:51 --*/

    /*           _               _
      ___  _   _| |_ _ __  _   _| |_
     / _ \| | | | __| `_ \| | | | __|
    | (_) | |_| | |_| |_) | |_| | |_
     \___/ \__,_|\__| .__/ \__,_|\__|
                    |_|
    */

    %put &=_dnaNam;
    %put &=_dnaSex;

    _dnaNam = "Joyce","Louise","Alice","James","Thomas"
    _dnaSex = "F","F","F","M","M"


    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  _dnaNam = "Joyce","Louise","Alice","James","Thomas"                                                                   */
    /*  _dnaSex = "F","F","F","M","M"                                                                                         */
    /*                                                                                                                        */
    /*  SHIFT RMB                                                                                                             */
    /*                                                                                                                        */
    /*    WORK.dna_030lbJynDm total obs=19 23JUL2022:07:08:47                                                                 */
    /*                                                                                                                        */
    /*   obs    NAME       SEX    AGE    HEIGHT    WEIGHT     LOWER                                                           */
    /*                                                                                                                        */
    /*     1    Alfred      M      14     69.0      112.5    100.646                                                          */
    /*     2    Alice       F      13     56.5       84.0     52.150                                                          */
    /*     3    Barbara     F      13     65.3       98.0     87.066                                                          */
    /*     4    Carol       F      14     62.8      102.5     77.526                                                          */
    /*     5    Henry       M      14     63.5      102.5     80.228                                                          */
    /*     6    James       M      12     57.3       83.0     55.476                                                          */
    /*     7    Jane        F      12     59.8       84.5     65.678                                                          */
    /*     8    Janet       F      15     62.5      112.5     76.361                                                          */
    /*     9    Jeffrey     M      13     62.5       84.0     76.361                                                          */
    /*    10    John        M      12     59.0       99.5     62.445                                                          */
    /*    11    Joyce       F      11     51.3       50.5     29.883                                                          */
    /*    12    Judy        F      14     64.3       90.0     83.286                                                          */
    /*    13    Louise      F      12     56.3       77.0     51.315                                                          */
    /*    14    Mary        F      15     66.5      112.0     91.539                                                          */
    /*    15    Philip      M      16     72.0      150.0    111.223                                                          */
    /*    16    Robert      M      12     64.8      128.0     85.182                                                          */
    /*    17    Ronald      M      15     67.0      133.0     93.383                                                          */
    /*    18    Thomas      M      11     57.5       85.0     56.303                                                          */
    /*    19    William     M      15     66.5      112.0     91.539                                                          */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  COMMAND LINE MACRO FRQH                                                                                               */
    /*                                                                                                                        */
    /*  Frequency of sex*age dataset WORK.DNA_030LBJYNDM 23JUL2022:07:10:54                                                   */
    /*                                                                                                                        */
    /*  Number of Variable Levels                                                                                             */
    /*                                                                                                                        */
    /*  Variable      Levels                                                                                                  */
    /*  --------------------                                                                                                  */
    /*  SEX                2                                                                                                  */
    /*  AGE                6                                                                                                  */
    /*                                                                                                                        */
    /*                                         Cumulative    Cumulative                                                       */
    /*  SEX    AGE    Frequency     Percent     Frequency      Percent                                                        */
    /*  ---------------------------------------------------------------                                                       */
    /*  F       11           1        5.26             1         5.26                                                         */
    /*  F       12           2       10.53             3        15.79                                                         */
    /*  F       13           2       10.53             5        26.32                                                         */
    /*  F       14           2       10.53             7        36.84                                                         */
    /*  F       15           2       10.53             9        47.37                                                         */
    /*  M       11           1        5.26            10        52.63                                                         */
    /*  M       12           3       15.79            13        68.42                                                         */
    /*  M       13           1        5.26            14        73.68                                                         */
    /*  M       14           2       10.53            16        84.21                                                         */
    /*  M       15           2       10.53            18        94.74                                                         */
    /*  M       16           1        5.26            19       100.00                                                         */
    /*                                                                                                                        */
    /*  COMMAND MACRO CNTH NAME (RESULT IN PASTE BUFFER)                                                                      */
    /*                                                                                                                        */
    /*  -- Number of unique levels=19 for name from dna_030LbJynDm(obs=19) 23JUL2022:07:00:51 --                              */
    /*                                                                                                                        */
    /*                                                                                                                        */
    /*  COMMAND MACRO XPY input (RESULT IN PASTE BUFFER)                                                                      */
    /*   _                   _                                                                                                */
    /*  (_)_ __  _ __  _   _| |_                                                                                              */
    /*  | | `_ \| `_ \| | | | __|                                                                                             */
    /*  | | | | | |_) | |_| | |_                                                                                              */
    /*  |_|_| |_| .__/ \__,_|\__|                                                                                             */
    /*          |_|                                                                                                           */
    /*                                                                                                                        */
    /**************************************************************************************************************************/
