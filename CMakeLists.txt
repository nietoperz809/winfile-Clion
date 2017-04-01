cmake_minimum_required(VERSION 3.7)

project(winfile2)

set(CMAKE_C_STANDARD 90)

include_directories("inc")

ADD_DEFINITIONS(
        -DWIN32
        -DNDEBUG
        -D_WINDOWS
        -D_MBCS
        -D_X86_
        -DLFN
        -DSTRICT
        -DFASTMOVE
        -DLFNCLIPBOARD
        -DW3
        -DUNICODE
        -DUSELASTDOT
        -DMEMDOUBLE
        -DWINVER=0x0400
        -D_VC80_UPGRADE=0x0600
        -D_UNICODE)

set (MY_CFLAGS
        "/GS /analyze- /W3 /Gy /Zc:wchar_t /Zi /Gm- /Zc:inline /fp:precise /GF /WX- /Zc:forScope /Gz /Oy- /EHsc /nologo /diagnostics:classic")

set (CMAKE_C_FLAGS "${MY_CFLAGS}")

set(MY_LIBRARIES 
        odbc32.lib
        ntdll.lib
        comctl32.lib
        Shlwapi.lib
        kernel32.lib
        user32.lib
        gdi32.lib
        winspool.lib
        comdlg32.lib
        advapi32.lib
        shell32.lib
        ole32.lib
        oleaut32.lib
        uuid.lib)

set(SOURCE_FILES
        dbg.c
        fontsel.c
        largeic.c
        lfn.c
        lfnmisc.c
        lstrfns.c
        numfmt.c
        psdocurd.c
        suggest.c
        tbar.c
        treectl.c
        utilnt.c
        wfassoc.c
        wfchgnot.c
        wfcomman.c
        wfcopy.c
        wfdir.c
        wfdirrd.c
        wfdirsrc.c
        wfdlgs.c
        wfdlgs2.c
        wfdlgs3.c
        wfdos.c
        wfdrives.c
        wfext.c
        wffile.c
        wfinfo.c
        wfinit.c
        wfmem.c
        wfprint.c
        wfsearch.c
        wftree.c
        wfutil.c
        winfile.c
        wnetcaps.c)

set (LINKCMDS
        "/MANIFEST /NXCOMPAT /DYNAMICBASE /DEBUG:FULL /MACHINE:X86 /SAFESEH /INCREMENTAL:NO /SUBSYSTEM:WINDOWS /MANIFESTUAC:\"level='asInvoker' uiAccess='false'\" /ManifestFile:\"winfile2.exe.manifest\" /ERRORREPORT:PROMPT /NOLOGO /TLBID:1"
)

set(rc_flags
        "/D \"NDEBUG\" /D \"_VC80_UPGRADE=0x0600\" /D \"UNICODE\" /D \"UNICODE\" /l 0x0407 /nologo /fo\"res.res\""
)

set(CMAKE_RC_FLAGS "${rc_flags}")

add_executable(winfile2 ${SOURCE_FILES} res.rc)
set_target_properties(winfile2 PROPERTIES LINK_FLAGS_RELEASE "${LINKCMDS}")
target_link_libraries(winfile2 ${MY_LIBRARIES})

