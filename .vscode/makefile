BIN_LIB = CMPSYS
LIBLIST = $(BIN_LIB) SAMPLE
SHELL = /QOpensys/usr/bin/qsh

all: testpgm.sqlrpgle 
testpgm.sqlrpgle: screen1.dspf

%.sqlrpgle:
    system -s "CHGATR OBJ('./testpgm.sqlrpgle') ATR(*CCSID) VALUE(1252)
	liblist -a $(LIBLIST);
	system "CRTSQLRPLI OBJ($(BIN_LIB)/$*) SRCSTMF('./testpgm.sqlrpgle') COMMIT(*NONE) DBGVIEW(*SOURCE) OPTION (*EVENTF)"

%.dspf
    -system -qi "CRTSRCPF FILE($(BIN_LIB)/QDDSSRC) RCDLEN(112)"
	system "CPYFRMSTMF FROMSTMF('./screen1.dspf') TOMBR('/QSYS.lib/$(BIN_LIB).lib/QDDSSRC.file/$*.mbr') MBROPT(*REPLACE)"
	system -s "CRTDSPF FILE($(BIN_LIN)/$*) SRCFILE($(BIN_LIB)/QDDSSRC) SRCMBR($*)"