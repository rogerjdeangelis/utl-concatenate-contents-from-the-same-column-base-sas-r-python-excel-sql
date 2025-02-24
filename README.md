# utl-concatenate-contents-from-the-same-column-base-sas-r-python-excel-sql
Concatenate contents from the same column base sas r python excel sql 
    %let pgm=utl-concatenate-contents-from-the-same-column-base-sas-r-python-excel-sql;

    %stop_submission;

    Concatenate contents from the same column base sas r python excel sql

      SOLUTIONS

           1 r sql (no need to sort - uses sqllite function group_concat)
           2 base sas (need to pre sort?)

    sas communities
    https://tinyurl.com/bddj934b
    https://communities.sas.com/t5/SAS-Programming/concatenate-contents-from-the-same-column/m-p/959052#M374251

    github
    https://tinyurl.com/72u3axpp
    https://github.com/rogerjdeangelis/utl-concatenate-contents-from-the-same-column-base-sas-r-python-excel-sql/new/main


    /**************************************************************************************************************************/
    /*                       |                                         |                                                      */
    /*      INPUT            |  PROCESS                                |  OUTPUT                                              */
    /*      =====            |  =======                                |  ======                                              */
    /*                       |                                         |                                                      */
    /* SD1.HAVE              |                                         |                                                      */
    /*                       | 1 R PYTHON EXCEL SQL(ONLY R BELOW)      | R                                                    */
    /* ASSET            ID   | ===================================     |                                                      */
    /*                       |                                         | ID                                          ASSETS   */
    /* MUTUAL FUND       7   | proc datasets lib=sd1 nolist nodetails; |                                                      */
    /* NOTICE INVEST     7   |  delete want;                           | 5 CARD BASED, DEMAND INVEST, FIXED INVEST, SERVICE   */
    /* UNCATEGORISED     7   | run;quit;                               | 7        MUTUAL FUND, NOTICE INVEST, UNCATEGORISED   */
    /* CARD BASED        5   |                                         |                                                      */
    /* DEMAND INVEST     5   | %utl_rbeginx;                           |                                                      */
    /* FIXED INVEST      5   | parmcards4;                             | SAS                                                  */
    /* SERVICE           5   | library(haven)                          |                                                      */
    /*                       | library(sqldf)                          | R                                                    */
    /*                       | source("c:/oto/fn_tosas9x.R")           | O                                                    */
    /* options               | have<-read_sas("d:/sd1/have.sas7bdat")  | W                                                    */
    /*  validvarname=upcase; | want<-sqldf("                           | N                                                    */
    /* libname sd1 "d:/sd1"; | select                                  | A                                                    */
    /* data sd1.have;        |    id                                   | M                                                    */
    /*  informat asset $24.; |    ,group_concat(asset,', ') as assets  | E I                                                  */
    /*  input id asset &;    | from                                    | S D                     ASSETS                       */
    /* cards4;               |     have                                |                                                      */
    /* 7 MUTUAL FUND         | group                                   | 1 5 CARD BASED, DEMAND INVEST, FIXED INVEST, SERVICE */
    /* 7 NOTICE INVEST       |     by id                               | 2 7 MUTUAL FUND, NOTICE INVEST, UNCATEGORISED        */
    /* 7 UNCATEGORISED       | ")                                      |                                                      */
    /* 5 CARD BASED          | want                                    |                                                      */
    /* 5 DEMAND INVEST       | fn_tosas9x(                             |                                                      */
    /* 5 FIXED INVEST        |       inp    = want                     |                                                      */
    /* 5 SERVICE             |      ,outdsn ="want"                    |                                                      */
    /* ;;;;                  |      )                                  |                                                      */
    /* run;quit;             | ;;;;                                    |                                                      */
    /*                       | %utl_rendx;                             |                                                      */
    /*                       |                                         |                                                      */
    /*                       | proc print data=sd1.want;               |                                                      */
    /*                       | run;quit;                               |                                                      */
    /*                       | run;quit;                               |                                                      */
    /*                       |                                         |                                                      */
    /*                       |------------------------------------------------------------------------------------------------*/
    /*                       |                                         |                                                      */
    /*                       |                                         |                                                      */
    /*                       | 2 BASE SAS                              |                                                      */
    /*                       | ==========                              | ID                       ASSETS                      */
    /*                       |                                         |                                                      */
    /*                       | proc datasets nolist nodetails;         |  5    CARD BASED,DEMAND INVEST,FIXED INVEST,SERVICE  */
    /*                       |  delete want;                           |  7    MUTUAL FUND,NOTICE INVEST,UNCATEGORISED        */
    /*                       | run;quit;                               |                                                      */
    /*                       |                                         |                                                      */
    /*                       | proc sort data=sd1.have;                |                                                      */
    /*                       |  by id asset;                           |                                                      */
    /*                       | run;quit;                               |                                                      */
    /*                       |                                         |                                                      */
    /*                       | data want;                              |                                                      */
    /*                       | set sd1.have;                           |                                                      */
    /*                       | by id asset;                            |                                                      */
    /*                       | length assets $1000;                    |                                                      */
    /*                       | array T {100} $150 _temporary_;         |                                                      */
    /*                       | if first.id then do;                    |                                                      */
    /*                       |     call missing(of T[*]);              |                                                      */
    /*                       |     recnum=0;                           |                                                      */
    /*                       | end;                                    |                                                      */
    /*                       | if first.asset then do;                 |                                                      */
    /*                       |     recnum+1;                           |                                                      */
    /*                       |     T[recnum]=asset;                    |                                                      */
    /*                       | end;                                    |                                                      */
    /*                       | if last.id then do;                     |                                                      */
    /*                       |     assets=catx(',', of T[*]);          |                                                      */
    /*                       |     output;                             |                                                      */
    /*                       | end;                                    |                                                      */
    /*                       | keep id assets;                         |                                                      */
    /*                       | run;                                    |                                                      */
    /*                       |                                         |                                                      */
    /*                       | proc print data=want;                   |                                                      */
    /*                       | run;quit;                               |                                                      */
    /*                       |                                         |                                                      */
    /**************************************************************************************************************************/

    /*              _
      ___ _ __   __| |
     / _ \ `_ \ / _` |
    |  __/ | | | (_| |
     \___|_| |_|\__,_|

    */
