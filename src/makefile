CC=icc /Q+ /Ss+ /G5
CCDLLFLAGS=/Gd+ /Ge+ /O- 
DISTR=distr
# icc is buggy? ICC IS VERY BUGGY ;-))))))) so turn off optimiztion

all: install

dftables.exe: 
 $(CC) dftables.c
 dftables.exe >chartables.c

pcre.dll: dftables.exe
 $(CC) $(CCDLLFLAGS) /Fepcre.dll pcreposix.c maketables.c get.c study.c pcre.c pcrelib.def

pcre.lib: pcre.dll
 IMPLIB pcre.lib pcre.dll

libpcre.lib: pcre.dll
 ILIB libpcre.lib pcreposix.obj maketables.obj get.obj study.obj pcre.obj,

pcretest.exe: pcre.lib
  $(CC) /I.  pcretest.c pcre.lib /B"/Stack:8000000"

pcregrep.exe: pcre.lib
  $(CC) /I.  pcregrep.c pcre.lib /B"/Stack:8000000"

install: pcregrep.exe pcretest.exe libpcre.lib
 - @mkdir distr 2>nul
 - @mkdir distr\src 2>nul
 - @mkdir distr\doc 2>nul
 @cp  pcregrep.exe pcretest.exe pcre.dll pcre.lib libpcre.lib pcre.h ./distr 
 @cp  makefile pcrelib.def config.h pcre.h ./distr/src
 @cp  doc/html/*.html ./distr/doc

clean:
  rm *.lib *.dll *.obj *.exe -f

