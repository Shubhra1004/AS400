       ctl-opt debug option(*srcstmt: *nodebugio: *nounref);
      /if defined(*crtbndrpg)
         ctl-opt dftactgrp(*no) actgrp(*new) usrprf(*owner);
      /endif
       dcl-f SCREEN1 WorkStn IndDS(ScreenInd);

       dcl-ds psds PSDS;
          Pgm char(10) pos(1);
          WsID char(10) pos(244);
          User char(10) pos(254);
       end-ds;
       dcl-ds ScreenInd;
          F3        ind pos(03);
          nondiplay ind pos(31);

       end-ds;

       dcl-ds ds_empd   ExtName('EMPDATA') qualified inz end-ds;
       dcl-c SQL_SUCCESS const(0);

       ExSr $Main;
       *INLR = *On;

       BegSr $Main;
         nondiplay = *on;
          DoW F3 = *Off;
            Write Header;
            ExFmt EMPDATA;
            Select;
              When F3;
                Leave;
              Other;
                ExSr WriteData;
            EndSl;
          EndDo;
        EndSr;

        BegSr WriteData;
          Exec Sql
                Select *
                Into :ds_empd
                From EMPDATA
                Where EMPID = :EMPID;

                   NAME    = ds_empd.empname;
                   PHONE   = ds_empd.phone;
                   ADDRESS = ds_empd.address;
                   ROLE    = ds_empd.postion;
                   MANAGR  = ds_empd.manager;
            nondiplay = *Off;

        EndSr;
