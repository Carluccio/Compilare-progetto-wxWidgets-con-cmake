#-------------------------------------------------------------------
# Per generare makefile del programma Archivio
# Scritto da Carlo Sala il 13/10/2014
#-------------------------------------------------------------------
cmake_minimum_required(VERSION 2.8.11)
project("${PRO}")
set(CMAKE_COLOR_MAKEFILE ON)
set(CMAKE_VERBOSE_MAKEFILE OFF)
set(VERS ${VERS})
set(M ${M})
set(S ${S})
add_definitions(${Z})
IF(${SQ1} MATCHES "n")
set(pathSq "")
ELSE(${SQ1} MATCHES "n")
include_directories(${SQ1}/include)
set(pathSq "-L${SQ1}/lib/gcc_${S}${R}")  # linker library wxWidgets non inserire C:/
set(LIBRARIES_SQ
wxsqlite3_msw${VERS}u${M}
)
ENDIF(${SQ1} MATCHES "n")
IF(${WX1} MATCHES "n")
set(pathWx "")
ELSE(${WX1} MATCHES "n")
include_directories(
	.
	${WX1}/include
	${WX1}/lib/gcc_${S}${R}/mswu${M}
)
set(pathWx "-L${WX1}/lib/gcc_${S}${R}")  # linker library wxWidgets non inserire C:/
set(LIBRARIES
wxmsw${VERS}u${M}_core
wxbase${VERS}u${M}
wxbase${VERS}u${M}_net
wxbase${VERS}u${M}_xml
wxexpat
wxjpeg
wxmsw${VERS}u${M}_adv
wxmsw${VERS}u${M}_aui
wxmsw${VERS}u${M}_gl
wxmsw${VERS}u${M}_html
wxmsw${VERS}u${M}_media
wxmsw${VERS}u${M}_propgrid
wxmsw${VERS}u${M}_ribbon
wxmsw${VERS}u${M}_richtext
wxmsw${VERS}u${M}_stc
wxmsw${VERS}u${M}_webview
wxmsw${VERS}u${M}_xrc
wxpng
wxregexu${M}
wxscintilla
wxtiff
wxzlib
)
ENDIF(${WX1} MATCHES "n")
set(path1 "")
set(path2 "")
set(path3 "")
set(LIBRARIES_SYSTEM
#------System------------------------------------
kernel32
user32
gdi32
comdlg32
winspool
winmm
shell32
shlwapi
comctl32
ole32
oleaut32
uuid
rpcrt4
advapi32
version
wsock32
wininet
oleacc
uxtheme
#----------------------------------------------------
)
# Linker e linker options
set(CMAKE_CXX_FLAGS  "${Y} ${CMAKE_CXX_FLAGS}")
set(CMAKE_EXE_LINKER_FLAGS "${J} ${CMAKE_EXE_LINKER_FLAGS} ${pathSq} ${pathWx}  ${path1} ${path2} ${path3}")
# Define the CXX sources
set(SRCS ${SORG1} ${SORG2} ${SORG3} ${SORG4} ${SORG5} ${SORG6} ${RESU})
  SET(CMAKE_RUNTIME_OUTPUT_DIRECTORY "${CAR}")
 #aggiunta da me 22/02/2016
 IF((${R} MATCHES "_dll") OR (${R} MATCHES "_lib"))
 SET(CMAKE_ RC_COMPILER windres.exe)
 ELSE()
 SET(CMAKE_RC_FLAGS "-F pe-i386")
 SET(CMAKE_RC_COMPILER windres.exe )
 ENDIF() 
   #fine aggiunta  
  ADD_EXECUTABLE(${PRO} ${SRCS})
   # and for each of your dependant executable/library targets:
TARGET_LINK_LIBRARIES(${PRO} "-Wl,--start-group;" ${LIBRARIES_SQ} ${LIBRARIES} "-Wl,--end-group;" ${LIBRARIES_SYSTEM})
#---------------------------FINE-------------------------------------------
