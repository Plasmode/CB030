##Getting Started with CB030 Rev1

#Introduction

This guide assume you already have a fully assembled CB030 rev1 as shown in the picture above.

Connecting console serial port
The console serial port is the CP2102 USB-serial adapter soldered directly to the CB030 board. Set the terminal emulator to 38400 N-8-1. Hardware handshake is not absolute required to operate CB030; the processor is fast enough to support Kermit file transfer without handware handshake.

Powering Up
CB030 requires regulated 5V, 1amp. The power plug is 2.5mm X 5.5mm which is not compatible with the more popular 2.1mm X 5.5mm connector.

Apply power to CB030 and the following message will display after about 1 second delay:

CB030Bug
2/26/20 v0.5, type “he” for help
>

Type 'he' to display the help menu

> he Commands are in lower case, <>optional, []mandatory dm [address] <count> dr <a|d|a0-a7|d0-d7> Display all registers if no parameter mm [address] <value> If only address entered, a submenu will follow: . terminates submenu session
- go back one word address
[value] modify current address and display next address
CR not modify current address but display next address
mr [a0-a7|d0-d7] <value> If only register entered, a submenu will follow:
. terminates submenu session
- go back one register
[value] modify current register and display next register
CR not modify current register but display next register
go <from_addr> <to_addr> If no address specified, use save register values
bp <addr> If no address specified, display current break point
special case: bp 0 removes breakpoint
du [address] <line count> dump specified number of lines
bo boot into CP/M68K, same as “go 15000”
eh start EhBasic, same as “go 4196”
>

Please refer to CB030 Monitor manual for description of various monitor commands.

CP/M68K
To run CP/M68K from the monitor, type 'bo' and the CP/M68K A> prompt will display

Drive A is read-only drive reside on EPROM. It contains the formatting software, 'init.68k' and file transfer file, 'gkermit.68k'

Drive B-E are 8-megabyte read-write drives reside on compact flash disk. The assembled and tested CB030 includes a CF disk already formated and loaded with CP/M68K distribution files.

A new blank CF disk needs to be formated first and then loaded with CP/M68K files. Since drive A already has the init.68k and gkermit.68k, it is easy to format and transfer files to a new CF disk.

To format a new CF disk, type:

init b:

init c:

init d:

init e:

CP/M will ask you to confirm, press 'y' to go ahead with the format command

To transfer file(s) with gkermit to a read-write drive (drive E in this example), type:

e:

a:gkermit -r

Select kermit protocol in your serial terminator emulator and send one or more files (in TeraTerm: File → Transfer → Kermit → Send, then pick the file or files to send).

Test drive CB030
First, change to a new drive and copy CP/M files to it:

pip b:=e:*.*[v] ← this command copies all files from drive E to drive B with verify

To run microEMACS, type:

me hello.c

The microEMACS screen editor will open with a blank screen, type:

main()

{

printf(“Hello World”);

}

ctrl-Z to save and exit microEMACS

To compile the Hello World program, type:

c hello

To link the Hello World program, type:

clink hello

to run the new Hello World program, type:

hello

The CP/M distribution include a simple BASIC program, asciiart.bas. To compile this BASIC program, type:

cb68 asciiart.bas

To link with BASIC library, type:

link68 asciiart,cb68.l68

To run the new BASIC program, type:

asciiart

You should see the following:
```
000000011111111111111111122222233347E7AB322222111100000000000000000000000000000
000001111111111111111122222222333557BF75433222211111000000000000000000000000000
000111111111111111112222222233445C      643332222111110000000000000000000000000
011111111111111111222222233444556C      654433332211111100000000000000000000000
11111111111111112222233346 D978 BCF    DF9 6556F4221111110000000000000000000000
111111111111122223333334469                 D   6322111111000000000000000000000
1111111111222333333334457DB                    85332111111100000000000000000000
11111122234B744444455556A                      96532211111110000000000000000000
122222233347BAA7AB776679                         A32211111110000000000000000000
2222233334567        9A                         A532221111111000000000000000000
222333346679                                    9432221111111000000000000000000
234445568  F                                   B5432221111111000000000000000000
                                              864332221111111000000000000000000
234445568  F                                   B5432221111111000000000000000000
222333346679                                    9432221111111000000000000000000
2222233334567        9A                         A532221111111000000000000000000
122222233347BAA7AB776679                         A32211111110000000000000000000
11111122234B744444455556A                      96532211111110000000000000000000
1111111111222333333334457DB                    85332111111100000000000000000000
111111111111122223333334469                 D   6322111111000000000000000000000
11111111111111112222233346 D978 BCF    DF9 6556F4221111110000000000000000000000
011111111111111111222222233444556C      654433332211111100000000000000000000000
000111111111111111112222222233445C      643332222111110000000000000000000000000
000001111111111111111122222222333557BF75433222211111000000000000000000000000000
000000011111111111111111122222233347E7AB322222111100000000000000000000000000000
