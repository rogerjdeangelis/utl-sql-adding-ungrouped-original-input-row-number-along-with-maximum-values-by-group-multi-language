# utl-sql-adding-ungrouped-original-input-row-number-along-with-maximum-values-by-group-multi-language
SQL adding ungrouped original input table row number along with maximum values by group multi language
    %let pgm=utl-sql-adding-ungrouped-original-input-row-number-along-with-maximum-values-by-group-multi-language;

    %stop_submission;

    SQL adding ungrouped original input table row number along with maximum values by group multi language

      SOLUTIONS ( you do need to specify what you want done with ties)

             1 sas sql
             2 r sql
             3 python sql

    github
    https://tinyurl.com/4w7b6a25
    https://github.com/rogerjdeangelis/utl-sql-adding-ungrouped-original-input-row-number-along-with-maximum-values-by-group-multi-language

    related to
    https://tinyurl.com/33e3v8nc
    https://stackoverflow.com/questions/79093903/find-maximum-values-for-each-month-and-keep-information-from-other-columns-in-da

    /*******************************************************************************************************************/
    /*                           |                                                  |                                  */
    /*         INPUT             |                 PROCESS                          |           OUTPUT                 */
    /*         =====             | SQL SELF EXPLANATORY EXACT SAME CODE IN R PYTHON |        ======                    */
    /*                           | =================================================|                                  */
    /*  REC   DATE     MTH SALES |                                                  |  REC     DATE    MTH SALESMAX    */
    /*                           |  SELECT                                          |                                  */
    /*  001  2011-01   01    24  |      MAX SALES                                   |  028    2020-01   1     99       */
    /*  002  2011-02   02    36  |      MONTH                                       |  011    2014-02   2     44       */
    /*  003  2011-03   03    38  |      DATE OF MAX SALES                           |  003    2011-03   3     38       */
    /*  004  2012-01   01    55  |      ROW NUMBER OF MAX SALES                     |                                  */
    /*  005  2012-02   02    28  |                                                  |                                  */
    /*  006  2012-03   03    21  |  select                                          |                                  */
    /*  007  2013-01   01    28  |     org.rec                                      |                                  */
    /*  008  2013-02   02    13  |    ,org.date                                     |                                  */
    /*  009  2013-03   03    22  |    ,org.mth                                      |                                  */
    /*  010  2014-01   01    24  |    ,grp.salesMax                                 |                                  */
    /*  011  2014-02   02    44  |  from                                            |                                  */
    /*  012  2014-03   03    13  |    sd1.have org join                             |                                  */
    /*  013  2015-01   01    66  |     /* SELECT MONTH AND MAX SALES FIRST */       |                                  */
    /*  014  2015-02   02    40  |      (                                           |                                  */
    /*  015  2015-03   03    13  |       select                                     |                                  */
    /*  016  2016-01   01    23  |         mth,                                     |                                  */
    /*  017  2016-02   02    26  |         max(sales) as salesMax                   |                                  */
    /*  018  2016-03   03    24  |       from                                       |                                  */
    /*  019  2017-01   01    41  |         sd1.have                                 |                                  */
    /*  020  2017-02   02     1  |       group                                      |                                  */
    /*  021  2017-03   03    28  |         by mth                                   |                                  */
    /*  022  2018-01   01    53  |      )  as grp                                   |                                  */
    /*  023  2018-02   02    20  |    /* MATCH TO ORIGINAL DATA FOR DATE AND REC */ |                                  */
    /*  024  2018-03   03    22  |    /* WHERE ORIGINAL MONTH = GROUP MONTH      */ |                                  */
    /*  025  2019-01   01    39  |    /* AND ORIGINAL SALES = GROUP MAX SALES    */ |                                  */
    /*  026  2019-02   02    28  |  on                                              |                                  */
    /*  027  2019-03   03    28  |          org.mth       = grp.mth                 |                                  */
    /*  028  2020-01   01    99  |     and  org.sales     = grp.salesMax            |                                  */
    /*  029  2020-02   02    29  |                                                  |                                  */
    /*  030  2020-03   03    17  |                                                  |                                  */
    /*                           |   DATA DOES NOT HAVE TO BE SORTED.               |                                  */
    /*                           |   SORTED FOR DOCUMENTATION PURPOSES              |                                  */
    /*                           |                                                  |                                  */
    /*                           |   REC     DATE      MTH    SALES                 |                                  */
    /*                           |                                                  |                                  */
    /*                           |   016    2016-01     1       23                  |                                  */
    /*                           |   001    2011-01     1       24                  |                                  */
    /*                           |   010    2014-01     1       24                  |                                  */
    /*                           |   007    2013-01     1       28                  |                                  */
    /*                           |   025    2019-01     1       39                  |                                  */
    /*                           |   019    2017-01     1       41                  |                                  */
    /*                           |   022    2018-01     1       53                  |                                  */
    /*                           |   004    2012-01     1       55                  |                                  */
    /*                           |   013    2015-01     1       66                  |                                  */
    /*                           |   028    2020-01     1       99 MAX              |                                  */
    /*                           |                                                  |                                  */
    /*                           |   020    2017-02     2        1                  |                                  */
    /*                           |   008    2013-02     2       13                  |                                  */
    /*                           |   023    2018-02     2       20                  |                                  */
    /*                           |   017    2016-02     2       26                  |                                  */
    /*                           |   005    2012-02     2       28                  |                                  */
    /*                           |   026    2019-02     2       28                  |                                  */
    /*                           |   029    2020-02     2       29                  |                                  */
    /*                           |   002    2011-02     2       36                  |                                  */
    /*                           |   014    2015-02     2       40                  |                                  */
    /*                           |   011    2014-02     2       44 MAX              |                                  */
    /*                           |                                                  |                                  */
    /*                           |   012    2014-03     3       13                  |                                  */
    /*                           |   015    2015-03     3       13                  |                                  */
    /*                           |   030    2020-03     3       17                  |                                  */
    /*                           |   006    2012-03     3       21                  |                                  */
    /*                           |   009    2013-03     3       22                  |                                  */
    /*                           |   024    2018-03     3       22                  |                                  */
    /*                           |   018    2016-03     3       24                  |                                  */
    /*                           |   021    2017-03     3       28                  |                                  */
    /*                           |   027    2019-03     3       28                  |                                  */
    /*                           |   003    2011-03     3       38 MAX              |                                  */
    /*                           |                                                  |                                  */
    /*******************************************************************************************************************/

    /*                   _
    (_)_ __  _ __  _   _| |_
    | | `_ \| `_ \| | | | __|
    | | | | | |_) | |_| | |_
    |_|_| |_| .__/ \__,_|\__|
            |_|
    */

    options validvarname=upcase;
    libname sd1 "d:/sd1";
    data sd1.have;
      input rec$ date$ mth sales;
    cards4;
    001 2011-01 01 24
    002 2011-02 02 36
    003 2011-03 03 38
    004 2012-01 01 55
    005 2012-02 02 28
    006 2012-03 03 21
    007 2013-01 01 28
    008 2013-02 02 13
    009 2013-03 03 22
    010 2014-01 01 24
    011 2014-02 02 44
    012 2014-03 03 13
    013 2015-01 01 66
    014 2015-02 02 40
    015 2015-03 03 13
    016 2016-01 01 23
    017 2016-02 02 26
    018 2016-03 03 24
    019 2017-01 01 41
    020 2017-02 02 1
    021 2017-03 03 28
    022 2018-01 01 53
    023 2018-02 02 20
    024 2018-03 03 22
    025 2019-01 01 39
    026 2019-02 02 28
    027 2019-03 03 28
    028 2020-01 01 99
    029 2020-02 02 29
    030 2020-03 03 17
    ;;;;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*   REC     DATE      MTH    SALES                                                                                       */
    /*                                                                                                                        */
    /*   001    2011-01     1       24                                                                                        */
    /*   002    2011-02     2       36                                                                                        */
    /*   003    2011-03     3       38                                                                                        */
    /*   004    2012-01     1       55                                                                                        */
    /*   005    2012-02     2       28                                                                                        */
    /*   006    2012-03     3       21                                                                                        */
    /*   007    2013-01     1       28                                                                                        */
    /*   008    2013-02     2       13                                                                                        */
    /*   009    2013-03     3       22                                                                                        */
    /*   010    2014-01     1       24                                                                                        */
    /*   011    2014-02     2       44                                                                                        */
    /*   012    2014-03     3       13                                                                                        */
    /*   013    2015-01     1       66                                                                                        */
    /*   014    2015-02     2       40                                                                                        */
    /*   015    2015-03     3       13                                                                                        */
    /*   016    2016-01     1       23                                                                                        */
    /*   017    2016-02     2       26                                                                                        */
    /*   018    2016-03     3       24                                                                                        */
    /*   019    2017-01     1       41                                                                                        */
    /*   020    2017-02     2        1                                                                                        */
    /*   021    2017-03     3       28                                                                                        */
    /*   022    2018-01     1       53                                                                                        */
    /*   023    2018-02     2       20                                                                                        */
    /*   024    2018-03     3       22                                                                                        */
    /*   025    2019-01     1       39                                                                                        */
    /*   026    2019-02     2       28                                                                                        */
    /*   027    2019-03     3       28                                                                                        */
    /*   028    2020-01     1       99                                                                                        */
    /*   029    2020-02     2       29                                                                                        */
    /*   030    2020-03     3       17                                                                                        */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*                             _
    / |  ___  __ _ ___   ___  __ _| |
    | | / __|/ _` / __| / __|/ _` | |
    | | \__ \ (_| \__ \ \__ \ (_| | |
    |_| |___/\__,_|___/ |___/\__, |_|
                                |_|
    */

    proc sql;
    create
       table want as
    select
       org.rec
      ,org.date
      ,org.mth
      ,grp.salesMax
    from
       sd1.have org join
       /* select monyh and max amount */
        (
         select
           mth,
           max(sales) as salesMax
         from
           sd1.have
         group
           by mth
        )  as grp
      /* match to original data for date and rec */
      on
            org.mth   = grp.mth
       and  org.sales = grp.salesMax
    order
       by org.mth
    ;quit;

    proc print data=want;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /* REC     DATE      MTH    SALESMAX                                                                                      */
    /*                                                                                                                        */
    /* 028    2020-01     1        99                                                                                         */
    /* 011    2014-02     2        44                                                                                         */
    /* 003    2011-03     3        38                                                                                         */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*___                     _
    |___ \   _ __   ___  __ _| |
      __) | | `__| / __|/ _` | |
     / __/  | |    \__ \ (_| | |
    |_____| |_|    |___/\__, |_|
                           |_|
    */

    %utl_rbeginx;
    parmcards4;
    library(sqldf)
    library(haven)
    source("c:/oto/fn_tosas9x.r")
    have<-read_sas("d:/sd1/have.sas7bdat")
    want <- sqldf('
       select
          org.rec
         ,org.date
         ,org.mth
         ,grp.salesMax
       from
          have org join
           (
            select
              mth,
              max(sales) as salesMax
            from
              have
            group
              by mth
           )  as grp
         on
               org.mth       = grp.mth
          and  org.sales     = grp.salesMax
       order
          by org.mth
       ');
    want;
    fn_tosas9x(
          inp    = want
         ,outlib ="d:/sd1/"
         ,outdsn ="rwant"
         )
    ;;;;
    %utl_rendx;

    proc print data=sd1.rwant;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  R                              SAS                                                                                    */
    /*                                                                                                                        */
    /*   REC    DATE MTH SALESMAX      ROWNAMES    REC     DATE      MTH    SALESMAX                                          */
    /*                                                                                                                        */
    /* 1 028 2020-01   1       99          1       028    2020-01     1        99                                             */
    /* 2 011 2014-02   2       44          2       011    2014-02     2        44                                             */
    /* 3 003 2011-03   3       38          3       003    2011-03     3        38                                             */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*____               _   _                             _
    |___ /   _ __  _   _| |_| |__   ___  _ __    ___  __ _| |
      |_ \  | `_ \| | | | __| `_ \ / _ \| `_ \  / __|/ _` | |
     ___) | | |_) | |_| | |_| | | | (_) | | | | \__ \ (_| | |
    |____/  | .__/ \__, |\__|_| |_|\___/|_| |_| |___/\__, |_|
            |_|    |___/                                |_|
    */

    proc datasets lib=sd1 nolist nodetails;
     delete pywant;
    run;quit;

    %utl_pybeginx;
    parmcards4;
    exec(open('c:/oto/fn_python.py').read());
    have,meta = ps.read_sas7bdat('d:/sd1/have.sas7bdat');
    want=pdsql('''
       select
          org.rec
         ,org.date
         ,org.mth
         ,grp.salesMax
       from
          have org join
           (
            select
              mth,
              max(sales) as salesMax
            from
              have
            group
              by mth
           )  as grp
         on
               org.mth       = grp.mth
          and  org.sales     = grp.salesMax
       order
          by org.mth
       ''');
    print(want);
    fn_tosas9x(want,outlib='d:/sd1/',outdsn='pywant',timeest=3);
    ;;;;
    %utl_pyendx;

    proc print data=sd1.pywant;
    run;quit;

    /**************************************************************************************************************************/
    /*                                                                                                                        */
    /*  PYTHON                               SAS                                                                              */
    /*                                                                                                                        */
    /*     REC     DATE  MTH  SALESMAX       REC     DATE      MTH    SALESMAX                                                */
    /*                                                                                                                        */
    /*  0  028  2020-01  1.0      99.0       028    2020-01     1        99                                                   */
    /*  1  011  2014-02  2.0      44.0       011    2014-02     2        44                                                   */
    /*  2  003  2011-03  3.0      38.0       003    2011-03     3        38                                                   */
    /*                                                                                                                        */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
