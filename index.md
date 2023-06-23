---
description: Top (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: Top (Debugging with GDB)
lang: en
resource-type: document
title: Top (Debugging with GDB)
---
# Debugging with [GDB]

This file documents the [GNU].

This is the Tenth Edition, of Debugging with [GDB] (GDB) Version 14.0.50.20230622-git.

Copyright © 1988-2023 Free Software Foundation, Inc.

Permission is granted to copy, distribute and/or modify this document under the terms of the GNU Free Documentation License, Version 1.3 or any later version published by the Free Software Foundation; with the Invariant Sections being "Free Software" and "Free Software Needs Free Documentation", with the Front-Cover Texts being "A GNU Manual," and with the Back-Cover Texts as in (a) below.

\(a\) The FSF's Back-Cover Text is: "You are free to copy and modify this GNU Manual. Buying copies from GNU Press supports the FSF in developing GNU and promoting software freedom."

::: header
Next: [Summary](Summary.html#Summary)]
:::

---

# Debugging with [GDB]

This file describes [GDB] symbolic debugger.

This is the Tenth Edition, for [GDB] (GDB) Version 14.0.50.20230622-git.

Copyright (C) 1988-2023 Free Software Foundation, Inc.

This edition of the GDB manual is dedicated to the memory of Fred Fish. Fred was a long-standing contributor to GDB and to Free software in general. We will miss him.

+:--------------------------------------------------------------------------------------------------------+-----------------------+:-----------------------------------------------------------------------------+
| • [Summary](Summary.html#Summary)                                                     |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Sample Session](Sample-Session.html#Sample-Session) session                                               |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| ``menu-comment                                                                                        |                       |                                                                              | |``                                                                                                     |                       |                                                                              |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Invocation](Invocation.html#Invocation)                                          |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Commands](Commands.html#Commands) commands                                                       |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Running](Running.html#Running)                                         |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Stopping](Stopping.html#Stopping):                                                    |                       | Stopping and continuing                                                      |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Reverse Execution](Reverse-Execution.html#Reverse-Execution):                         |                       | Running programs backward                                                    |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Process Record and Replay](Process-Record-and-Replay.html#Process-Record-and-Replay): |                       | Recording inferior's execution and replaying it                              |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Stack](Stack.html#Stack):                                                             |                       | Examining the stack                                                          |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Source](Source.html#Source):                                                                         |                       | Examining source files                                                       |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Data](Data.html#Data):                                                                               |                       | Examining data                                                               |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Optimized Code](Optimized-Code.html#Optimized-Code):                                                 |                       | Debugging optimized code                                                     |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Macros](Macros.html#Macros):                                                                         |                       | Preprocessor Macros                                                          |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Tracepoints](Tracepoints.html#Tracepoints):                                                          |                       | Debugging remote targets non-intrusively                                     |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Overlays](Overlays.html#Overlays):                                                                   |                       | Debugging programs that use overlays                                         |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| ``menu-comment                                                                                        |                       |                                                                              | |``                                                                                                     |                       |                                                                              |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Languages](Languages.html#Languages):                                                                |                       | Using [GDB] with different languages                                 |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| ``menu-comment                                                                                        |                       |                                                                              | |``                                                                                                     |                       |                                                                              |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Symbols](Symbols.html#Symbols):                                                                      |                       | Examining the symbol table                                                   |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Altering](Altering.html#Altering):                                                                   |                       | Altering execution                                                           |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [GDB Files](GDB-Files.html#GDB-Files):                                                                |                       | [GDB] files                                                          |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Targets](Targets.html#Targets):                                                                      |                       | Specifying a debugging target                                                |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Remote Debugging](Remote-Debugging.html#Remote-Debugging):                                           |                       | Debugging remote programs                                                    |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Configurations](Configurations.html#Configurations):                                                 |                       | Configuration-specific information                                           |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Controlling GDB](Controlling-GDB.html#Controlling-GDB):                                              |                       | Controlling [GDB]                                                    |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Extending GDB](Extending-GDB.html#Extending-GDB):                                                    |                       | Extending [GDB]                                                      |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Interpreters](Interpreters.html#Interpreters):                                                       |                       | Command Interpreters                                                         |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [TUI](TUI.html#TUI):                                                                                  |                       | [GDB] Text User Interface                                            |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Emacs](Emacs.html#Emacs):                                                                            |                       | Using [GDB] Emacs                                |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [GDB/MI](GDB_002fMI.html#GDB_002fMI):                                                                 |                       | [GDB]'s Machine Interface.                                           |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Annotations](Annotations.html#Annotations):                                                          |                       | [GDB]'s annotation interface.                                        |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Debugger Adapter Protocol](Debugger-Adapter-Protocol.html#Debugger-Adapter-Protocol):                |                       | The Debugger Adapter Protocol.                                               |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [JIT Interface](JIT-Interface.html#JIT-Interface):                                                    |                       | Using the JIT debugging interface.                                           |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [In-Process Agent](In_002dProcess-Agent.html#In_002dProcess-Agent):                                   |                       | In-Process Agent                                                             |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| ``menu-comment                                                                                        |                       |                                                                              | |``                                                                                                     |                       |                                                                              |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [GDB Bugs](GDB-Bugs.html#GDB-Bugs):                                                                   |                       | Reporting bugs in [GDB]                                              |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| ``menu-comment                                                                                        |                       |                                                                              | |``                                                                                                     |                       |                                                                              |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Command Line Editing](Command-Line-Editing.html#Command-Line-Editing):                               |                       | Command Line Editing                                                         |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Using History Interactively](Using-History-Interactively.html#Using-History-Interactively):          |                       | Using History Interactively                                                  |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [In Memoriam](In-Memoriam.html#In-Memoriam):                                                          |                       | In Memoriam                                                                  |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Formatting Documentation](Formatting-Documentation.html#Formatting-Documentation):                   |                       | How to format and print [GDB] documentation                          |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Installing GDB](Installing-GDB.html#Installing-GDB):                                                 |                       | Installing [GDB]                                                     |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Maintenance Commands](Maintenance-Commands.html#Maintenance-Commands):                               |                       | Maintenance Commands                                                         |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Remote Protocol](Remote-Protocol.html#Remote-Protocol):                                              |                       | GDB Remote Serial Protocol                                                   |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Agent Expressions](Agent-Expressions.html#Agent-Expressions):                                        |                       | The [GDB] Agent Expression Mechanism                                 |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Target Descriptions](Target-Descriptions.html#Target-Descriptions):                                  |                       | How targets can describe themselves to [GDB]                         |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Operating System Information](Operating-System-Information.html#Operating-System-Information):       |                       | Getting additional information from the operating system                     |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Trace File Format](Trace-File-Format.html#Trace-File-Format):                                        |                       | [GDB] trace file format                                              |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Index Section Format](Index-Section-Format.html#Index-Section-Format):                               |                       | .gdb_index section format                                                    |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Debuginfod](Debuginfod.html#Debuginfod):                                                             |                       | Download debugging resources with `debuginfod`                               |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Man Pages](Man-Pages.html#Man-Pages):                                                                |                       | Manual pages                                                                 |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Copying](Copying.html#Copying):                                                                      |                       | GNU General Public License says how you can copy and share [GDB]     |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [GNU Free Documentation License](GNU-Free-Documentation-License.html#GNU-Free-Documentation-License): |                       | The license for this documentation                                           |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Concept Index](Concept-Index.html#Concept-Index):                                                    |                       | Index of [GDB] concepts                                              |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+
| • [Command and Variable Index](Command-and-Variable-Index.html#Command-and-Variable-Index):             |                       | Index of [GDB] commands, variables, functions, and Python data types |
+---------------------------------------------------------------------------------------------------------+-----------------------+------------------------------------------------------------------------------+

## Table of Contents

::: contents

- [Summary of [GDB]
  - [Free Software](Free-Software.html#Free-Software)
  - [Free Software Needs Free Documentation](Free-Documentation.html#Free-Documentation)
  - [Contributors to [GDB]
- [1 A Sample [GDB]
- [2 Getting In and Out of [GDB]
  - [2.1 Invoking [GDB]
    - [2.1.1 Choosing Files](File-Options.html#File-Options)
    - [2.1.2 Choosing Modes](Mode-Options.html#Mode-Options)
    - [2.1.3 What [GDB]
    - [2.1.4 Initialization Files](Initialization-Files.html#Initialization-Files)
      - [2.1.4.1 Home directory early initialization files](Initialization-Files.html#Home-directory-early-initialization-files)
      - [2.1.4.2 System wide initialization files](Initialization-Files.html#System-wide-initialization-files)
      - [2.1.4.3 Home directory initialization file](Initialization-Files.html#Home-directory-initialization-file)
      - [2.1.4.4 Local directory initialization file](Initialization-Files.html#Local-directory-initialization-file)
  - [2.2 Quitting [GDB]
  - [2.3 Shell Commands](Shell-Commands.html#Shell-Commands)
  - [2.4 Logging Output](Logging-Output.html#Logging-Output)
- [3 [GDB]
  - [3.1 Command Syntax](Command-Syntax.html#Command-Syntax)
  - [3.2 Command Settings](Command-Settings.html#Command-Settings)
  - [3.3 Command Completion](Completion.html#Completion)
  - [3.4 Command options](Command-Options.html#Command-Options)
  - [3.5 Getting Help](Help.html#Help)
- [4 Running Programs Under [GDB]
  - [4.1 Compiling for Debugging](Compilation.html#Compilation)
  - [4.2 Starting your Program](Starting.html#Starting)
  - [4.3 Your Program's Arguments](Arguments.html#Arguments)
  - [4.4 Your Program's Environment](Environment.html#Environment)
  - [4.5 Your Program's Working Directory](Working-Directory.html#Working-Directory)
  - [4.6 Your Program's Input and Output](Input_002fOutput.html#Input_002fOutput)
  - [4.7 Debugging an Already-running Process](Attach.html#Attach)
  - [4.8 Killing the Child Process](Kill-Process.html#Kill-Process)
  - [4.9 Debugging Multiple Inferiors Connections and Programs](Inferiors-Connections-and-Programs.html#Inferiors-Connections-and-Programs)
  - [4.10 Debugging Programs with Multiple Threads](Threads.html#Threads)
  - [4.11 Debugging Forks](Forks.html#Forks)
  - [4.12 Setting a *Bookmark* to Return to Later](Checkpoint_002fRestart.html#Checkpoint_002fRestart)
    - [4.12.1 A Non-obvious Benefit of Using Checkpoints](Checkpoint_002fRestart.html#A-Non_002dobvious-Benefit-of-Using-Checkpoints)
- [5 Stopping and Continuing](Stopping.html#Stopping)
  - [5.1 Breakpoints, Watchpoints, and Catchpoints](Breakpoints.html#Breakpoints)
    - [5.1.1 Setting Breakpoints](Set-Breaks.html#Set-Breaks)
    - [5.1.2 Setting Watchpoints](Set-Watchpoints.html#Set-Watchpoints)
    - [5.1.3 Setting Catchpoints](Set-Catchpoints.html#Set-Catchpoints)
    - [5.1.4 Deleting Breakpoints](Delete-Breaks.html#Delete-Breaks)
    - [5.1.5 Disabling Breakpoints](Disabling.html#Disabling)
    - [5.1.6 Break Conditions](Conditions.html#Conditions)
    - [5.1.7 Breakpoint Command Lists](Break-Commands.html#Break-Commands)
    - [5.1.8 Dynamic Printf](Dynamic-Printf.html#Dynamic-Printf)
    - [5.1.9 How to save breakpoints to a file](Save-Breakpoints.html#Save-Breakpoints)
    - [5.1.10 Static Probe Points](Static-Probe-Points.html#Static-Probe-Points)
    - [5.1.11 "Cannot insert breakpoints"](Error-in-Breakpoints.html#Error-in-Breakpoints)
    - [5.1.12 "Breakpoint address adjusted\..."](Breakpoint_002drelated-Warnings.html#Breakpoint_002drelated-Warnings)
  - [5.2 Continuing and Stepping](Continuing-and-Stepping.html#Continuing-and-Stepping)
  - [5.3 Skipping Over Functions and Files](Skipping-Over-Functions-and-Files.html#Skipping-Over-Functions-and-Files)
  - [5.4 Signals](Signals.html#Signals)
  - [5.5 Stopping and Starting Multi-thread Programs](Thread-Stops.html#Thread-Stops)
    - [5.5.1 All-Stop Mode](All_002dStop-Mode.html#All_002dStop-Mode)
    - [5.5.2 Non-Stop Mode](Non_002dStop-Mode.html#Non_002dStop-Mode)
    - [5.5.3 Background Execution](Background-Execution.html#Background-Execution)
    - [5.5.4 Thread-Specific Breakpoints](Thread_002dSpecific-Breakpoints.html#Thread_002dSpecific-Breakpoints)
    - [5.5.5 Interrupted System Calls](Interrupted-System-Calls.html#Interrupted-System-Calls)
    - [5.5.6 Observer Mode](Observer-Mode.html#Observer-Mode)
- [6 Running programs backward](Reverse-Execution.html#Reverse-Execution)
- [7 Recording Inferior's Execution and Replaying It](Process-Record-and-Replay.html#Process-Record-and-Replay)
- [8 Examining the Stack](Stack.html#Stack)
  - [8.1 Stack Frames](Frames.html#Frames)
  - [8.2 Backtraces](Backtrace.html#Backtrace)
  - [8.3 Selecting a Frame](Selection.html#Selection)
  - [8.4 Information About a Frame](Frame-Info.html#Frame-Info)
  - [8.5 Applying a Command to Several Frames.](Frame-Apply.html#Frame-Apply)
  - [8.6 Management of Frame Filters.](Frame-Filter-Management.html#Frame-Filter-Management)
- [9 Examining Source Files](Source.html#Source)
  - [9.1 Printing Source Lines](List.html#List)
  - [9.2 Location Specifications](Location-Specifications.html#Location-Specifications)
    - [9.2.1 Linespec Locations](Linespec-Locations.html#Linespec-Locations)
    - [9.2.2 Explicit Locations](Explicit-Locations.html#Explicit-Locations)
    - [9.2.3 Address Locations](Address-Locations.html#Address-Locations)
  - [9.3 Editing Source Files](Edit.html#Edit)
    - [9.3.1 Choosing your Editor](Edit.html#Choosing-your-Editor)
  - [9.4 Searching Source Files](Search.html#Search)
  - [9.5 Specifying Source Directories](Source-Path.html#Source-Path)
  - [9.6 Source and Machine Code](Machine-Code.html#Machine-Code)
  - [9.7 Disable Reading Source Code](Disable-Reading-Source.html#Disable-Reading-Source)
- [10 Examining Data](Data.html#Data)
  - [10.1 Expressions](Expressions.html#Expressions)
  - [10.2 Ambiguous Expressions](Ambiguous-Expressions.html#Ambiguous-Expressions)
  - [10.3 Program Variables](Variables.html#Variables)
  - [10.4 Artificial Arrays](Arrays.html#Arrays)
  - [10.5 Output Formats](Output-Formats.html#Output-Formats)
  - [10.6 Examining Memory](Memory.html#Memory)
  - [10.7 Memory Tagging](Memory-Tagging.html#Memory-Tagging)
  - [10.8 Automatic Display](Auto-Display.html#Auto-Display)
  - [10.9 Print Settings](Print-Settings.html#Print-Settings)
  - [10.10 Pretty Printing](Pretty-Printing.html#Pretty-Printing)
    - [10.10.1 Pretty-Printer Introduction](Pretty_002dPrinter-Introduction.html#Pretty_002dPrinter-Introduction)
    - [10.10.2 Pretty-Printer Example](Pretty_002dPrinter-Example.html#Pretty_002dPrinter-Example)
    - [10.10.3 Pretty-Printer Commands](Pretty_002dPrinter-Commands.html#Pretty_002dPrinter-Commands)
  - [10.11 Value History](Value-History.html#Value-History)
  - [10.12 Convenience Variables](Convenience-Vars.html#Convenience-Vars)
  - [10.13 Convenience Functions](Convenience-Funs.html#Convenience-Funs)
  - [10.14 Registers](Registers.html#Registers)
  - [10.15 Floating Point Hardware](Floating-Point-Hardware.html#Floating-Point-Hardware)
  - [10.16 Vector Unit](Vector-Unit.html#Vector-Unit)
  - [10.17 Operating System Auxiliary Information](OS-Information.html#OS-Information)
  - [10.18 Memory Region Attributes](Memory-Region-Attributes.html#Memory-Region-Attributes)
    - [10.18.1 Attributes](Memory-Region-Attributes.html#Attributes)
      - [10.18.1.1 Memory Access Mode](Memory-Region-Attributes.html#Memory-Access-Mode)
      - [10.18.1.2 Memory Access Size](Memory-Region-Attributes.html#Memory-Access-Size)
      - [10.18.1.3 Data Cache](Memory-Region-Attributes.html#Data-Cache)
    - [10.18.2 Memory Access Checking](Memory-Region-Attributes.html#Memory-Access-Checking)
  - [10.19 Copy Between Memory and a File](Dump_002fRestore-Files.html#Dump_002fRestore-Files)
  - [10.20 How to Produce a Core File from Your Program](Core-File-Generation.html#Core-File-Generation)
  - [10.21 Character Sets](Character-Sets.html#Character-Sets)
  - [10.22 Caching Data of Targets](Caching-Target-Data.html#Caching-Target-Data)
  - [10.23 Search Memory](Searching-Memory.html#Searching-Memory)
  - [10.24 Value Sizes](Value-Sizes.html#Value-Sizes)
- [11 Debugging Optimized Code](Optimized-Code.html#Optimized-Code)
  - [11.1 Inline Functions](Inline-Functions.html#Inline-Functions)
  - [11.2 Tail Call Frames](Tail-Call-Frames.html#Tail-Call-Frames)
- [12 C Preprocessor Macros](Macros.html#Macros)
- [13 Tracepoints](Tracepoints.html#Tracepoints)
  - [13.1 Commands to Set Tracepoints](Set-Tracepoints.html#Set-Tracepoints)
    - [13.1.1 Create and Delete Tracepoints](Create-and-Delete-Tracepoints.html#Create-and-Delete-Tracepoints)
    - [13.1.2 Enable and Disable Tracepoints](Enable-and-Disable-Tracepoints.html#Enable-and-Disable-Tracepoints)
    - [13.1.3 Tracepoint Passcounts](Tracepoint-Passcounts.html#Tracepoint-Passcounts)
    - [13.1.4 Tracepoint Conditions](Tracepoint-Conditions.html#Tracepoint-Conditions)
    - [13.1.5 Trace State Variables](Trace-State-Variables.html#Trace-State-Variables)
    - [13.1.6 Tracepoint Action Lists](Tracepoint-Actions.html#Tracepoint-Actions)
    - [13.1.7 Listing Tracepoints](Listing-Tracepoints.html#Listing-Tracepoints)
    - [13.1.8 Listing Static Tracepoint Markers](Listing-Static-Tracepoint-Markers.html#Listing-Static-Tracepoint-Markers)
    - [13.1.9 Starting and Stopping Trace Experiments](Starting-and-Stopping-Trace-Experiments.html#Starting-and-Stopping-Trace-Experiments)
    - [13.1.10 Tracepoint Restrictions](Tracepoint-Restrictions.html#Tracepoint-Restrictions)
  - [13.2 Using the Collected Data](Analyze-Collected-Data.html#Analyze-Collected-Data)
    - [13.2.1 `tfind n`](tfind.html#tfind)
    - [13.2.2 `tdump`](tdump.html#tdump)
    - [13.2.3 `save tracepoints filename`](save-tracepoints.html#save-tracepoints)
  - [13.3 Convenience Variables for Tracepoints](Tracepoint-Variables.html#Tracepoint-Variables)
  - [13.4 Using Trace Files](Trace-Files.html#Trace-Files)
- [14 Debugging Programs That Use Overlays](Overlays.html#Overlays)
  - [14.1 How Overlays Work](How-Overlays-Work.html#How-Overlays-Work)
  - [14.2 Overlay Commands](Overlay-Commands.html#Overlay-Commands)
  - [14.3 Automatic Overlay Debugging](Automatic-Overlay-Debugging.html#Automatic-Overlay-Debugging)
  - [14.4 Overlay Sample Program](Overlay-Sample-Program.html#Overlay-Sample-Program)
- [15 Using [GDB]
  - [15.1 Switching Between Source Languages](Setting.html#Setting)
    - [15.1.1 List of Filename Extensions and Languages](Filenames.html#Filenames)
    - [15.1.2 Setting the Working Language](Manually.html#Manually)
    - [15.1.3 Having [GDB]
  - [15.2 Displaying the Language](Show.html#Show)
  - [15.3 Type and Range Checking](Checks.html#Checks)
    - [15.3.1 An Overview of Type Checking](Type-Checking.html#Type-Checking)
    - [15.3.2 An Overview of Range Checking](Range-Checking.html#Range-Checking)
  - [15.4 Supported Languages](Supported-Languages.html#Supported-Languages)
    - [15.4.1 C and C++](C.html#C)
      - [15.4.1.1 C and C++ Operators](C-Operators.html#C-Operators)
      - [15.4.1.2 C and C++ Constants](C-Constants.html#C-Constants)
      - [15.4.1.3 C++ Expressions](C-Plus-Plus-Expressions.html#C-Plus-Plus-Expressions)
      - [15.4.1.4 C and C++ Defaults](C-Defaults.html#C-Defaults)
      - [15.4.1.5 C and C++ Type and Range Checks](C-Checks.html#C-Checks)
      - [15.4.1.6 [GDB]
      - [15.4.1.7 [GDB]
      - [15.4.1.8 Decimal Floating Point format](Decimal-Floating-Point.html#Decimal-Floating-Point)
    - [15.4.2 D](D.html#D)
    - [15.4.3 Go](Go.html#Go)
    - [15.4.4 Objective-C](Objective_002dC.html#Objective_002dC)
      - [15.4.4.1 Method Names in Commands](Method-Names-in-Commands.html#Method-Names-in-Commands)
      - [15.4.4.2 The Print Command With Objective-C](The-Print-Command-with-Objective_002dC.html#The-Print-Command-with-Objective_002dC)
    - [15.4.5 OpenCL C](OpenCL-C.html#OpenCL-C)
      - [15.4.5.1 OpenCL C Datatypes](OpenCL-C-Datatypes.html#OpenCL-C-Datatypes)
      - [15.4.5.2 OpenCL C Expressions](OpenCL-C-Expressions.html#OpenCL-C-Expressions)
      - [15.4.5.3 OpenCL C Operators](OpenCL-C-Operators.html#OpenCL-C-Operators)
    - [15.4.6 Fortran](Fortran.html#Fortran)
      - [15.4.6.1 Fortran Types](Fortran-Types.html#Fortran-Types)
      - [15.4.6.2 Fortran Operators and Expressions](Fortran-Operators.html#Fortran-Operators)
      - [15.4.6.3 Fortran Intrinsics](Fortran-Intrinsics.html#Fortran-Intrinsics)
      - [15.4.6.4 Special Fortran Commands](Special-Fortran-Commands.html#Special-Fortran-Commands)
    - [15.4.7 Pascal](Pascal.html#Pascal)
    - [15.4.8 Rust](Rust.html#Rust)
    - [15.4.9 Modula-2](Modula_002d2.html#Modula_002d2)
      - [15.4.9.1 Operators](M2-Operators.html#M2-Operators)
      - [15.4.9.2 Built-in Functions and Procedures](Built_002dIn-Func_002fProc.html#Built_002dIn-Func_002fProc)
      - [15.4.9.3 Constants](M2-Constants.html#M2-Constants)
      - [15.4.9.4 Modula-2 Types](M2-Types.html#M2-Types)
      - [15.4.9.5 Modula-2 Defaults](M2-Defaults.html#M2-Defaults)
      - [15.4.9.6 Deviations from Standard Modula-2](Deviations.html#Deviations)
      - [15.4.9.7 Modula-2 Type and Range Checks](M2-Checks.html#M2-Checks)
      - [15.4.9.8 The Scope Operators `::` and `.`](M2-Scope.html#M2-Scope)
      - [15.4.9.9 [GDB]
    - [15.4.10 Ada](Ada.html#Ada)
      - [15.4.10.1 Introduction](Ada-Mode-Intro.html#Ada-Mode-Intro)
      - [15.4.10.2 Omissions from Ada](Omissions-from-Ada.html#Omissions-from-Ada)
      - [15.4.10.3 Additions to Ada](Additions-to-Ada.html#Additions-to-Ada)
      - [15.4.10.4 Overloading support for Ada](Overloading-support-for-Ada.html#Overloading-support-for-Ada)
      - [15.4.10.5 Stopping at the Very Beginning](Stopping-Before-Main-Program.html#Stopping-Before-Main-Program)
      - [15.4.10.6 Ada Exceptions](Ada-Exceptions.html#Ada-Exceptions)
      - [15.4.10.7 Extensions for Ada Tasks](Ada-Tasks.html#Ada-Tasks)
      - [15.4.10.8 Tasking Support when Debugging Core Files](Ada-Tasks-and-Core-Files.html#Ada-Tasks-and-Core-Files)
      - [15.4.10.9 Tasking Support when using the Ravenscar Profile](Ravenscar-Profile.html#Ravenscar-Profile)
      - [15.4.10.10 Ada Source Character Set](Ada-Source-Character-Set.html#Ada-Source-Character-Set)
      - [15.4.10.11 Known Peculiarities of Ada Mode](Ada-Glitches.html#Ada-Glitches)
  - [15.5 Unsupported Languages](Unsupported-Languages.html#Unsupported-Languages)
- [16 Examining the Symbol Table](Symbols.html#Symbols)
- [17 Altering Execution](Altering.html#Altering)
  - [17.1 Assignment to Variables](Assignment.html#Assignment)
  - [17.2 Continuing at a Different Address](Jumping.html#Jumping)
  - [17.3 Giving your Program a Signal](Signaling.html#Signaling)
  - [17.4 Returning from a Function](Returning.html#Returning)
  - [17.5 Calling Program Functions](Calling.html#Calling)
    - [17.5.1 Calling functions with no debug info](Calling.html#Calling-functions-with-no-debug-info)
  - [17.6 Patching Programs](Patching.html#Patching)
  - [17.7 Compiling and injecting code in [GDB]
    - [17.7.1 Compilation options for the `compile` command](Compiling-and-Injecting-Code.html#Compilation-options-for-the-compile-command)
    - [17.7.2 Caveats when using the `compile` command](Compiling-and-Injecting-Code.html#Caveats-when-using-the-compile-command)
    - [17.7.3 Compiler search for the `compile` command](Compiling-and-Injecting-Code.html#Compiler-search-for-the-compile-command)
- [18 [GDB]
  - [18.1 Commands to Specify Files](Files.html#Files)
  - [18.2 File Caching](File-Caching.html#File-Caching)
  - [18.3 Debugging Information in Separate Files](Separate-Debug-Files.html#Separate-Debug-Files)
  - [18.4 Debugging information in a special section](MiniDebugInfo.html#MiniDebugInfo)
  - [18.5 Index Files Speed Up [GDB]
    - [18.5.1 Automatic symbol index cache](Index-Files.html#Automatic-symbol-index-cache)
  - [18.6 Errors Reading Symbol Files](Symbol-Errors.html#Symbol-Errors)
  - [18.7 GDB Data Files](Data-Files.html#Data-Files)
- [19 Specifying a Debugging Target](Targets.html#Targets)
  - [19.1 Active Targets](Active-Targets.html#Active-Targets)
  - [19.2 Commands for Managing Targets](Target-Commands.html#Target-Commands)
  - [19.3 Choosing Target Byte Order](Byte-Order.html#Byte-Order)
- [20 Debugging Remote Programs](Remote-Debugging.html#Remote-Debugging)
  - [20.1 Connecting to a Remote Target](Connecting.html#Connecting)
    - [20.1.1 Types of Remote Connections](Connecting.html#Types-of-Remote-Connections)
    - [20.1.2 Host and Target Files](Connecting.html#Host-and-Target-Files)
    - [20.1.3 Remote Connection Commands](Connecting.html#Remote-Connection-Commands)
  - [20.2 Sending files to a remote system](File-Transfer.html#File-Transfer)
  - [20.3 Using the `gdbserver` Program](Server.html#Server)
    - [20.3.1 Running `gdbserver`](Server.html#Running-gdbserver-1)
      - [20.3.1.1 Attaching to a Running Program](Server.html#Attaching-to-a-Running-Program)
      - [20.3.1.2 TCP port allocation lifecycle of `gdbserver`](Server.html#TCP-port-allocation-lifecycle-of-gdbserver)
      - [20.3.1.3 Other Command-Line Arguments for `gdbserver`](Server.html#Other-Command_002dLine-Arguments-for-gdbserver-1)
    - [20.3.2 Connecting to `gdbserver`](Server.html#Connecting-to-gdbserver)
    - [20.3.3 Monitor Commands for `gdbserver`](Server.html#Monitor-Commands-for-gdbserver-1)
    - [20.3.4 Tracepoints support in `gdbserver`](Server.html#Tracepoints-support-in-gdbserver)
  - [20.4 Remote Configuration](Remote-Configuration.html#Remote-Configuration)
  - [20.5 Implementing a Remote Stub](Remote-Stub.html#Remote-Stub)
    - [20.5.1 What the Stub Can Do for You](Stub-Contents.html#Stub-Contents)
    - [20.5.2 What You Must Do for the Stub](Bootstrapping.html#Bootstrapping)
    - [20.5.3 Putting it All Together](Debug-Session.html#Debug-Session)
- [21 Configuration-Specific Information](Configurations.html#Configurations)
  - [21.1 Native](Native.html#Native)
    - [21.1.1 BSD libkvm Interface](BSD-libkvm-Interface.html#BSD-libkvm-Interface)
    - [21.1.2 Process Information](Process-Information.html#Process-Information)
    - [21.1.3 Features for Debugging [DJGPP]
    - [21.1.4 Features for Debugging MS Windows PE Executables](Cygwin-Native.html#Cygwin-Native)
      - [21.1.4.1 Support for DLLs without Debugging Symbols](Non_002ddebug-DLL-Symbols.html#Non_002ddebug-DLL-Symbols)
      - [21.1.4.2 DLL Name Prefixes](Non_002ddebug-DLL-Symbols.html#DLL-Name-Prefixes)
      - [21.1.4.3 Working with Minimal Symbols](Non_002ddebug-DLL-Symbols.html#Working-with-Minimal-Symbols)
    - [21.1.5 Commands Specific to [GNU]
    - [21.1.6 Darwin](Darwin.html#Darwin)
    - [21.1.7 FreeBSD](FreeBSD.html#FreeBSD)
  - [21.2 Embedded Operating Systems](Embedded-OS.html#Embedded-OS)
  - [21.3 Embedded Processors](Embedded-Processors.html#Embedded-Processors)
    - [21.3.1 Synopsys ARC](ARC.html#ARC)
    - [21.3.2 ARM](ARM.html#ARM)
    - [21.3.3 BPF](BPF.html#BPF)
    - [21.3.4 M68k](M68K.html#M68K)
    - [21.3.5 MicroBlaze](MicroBlaze.html#MicroBlaze)
    - [21.3.6 MIPS Embedded](MIPS-Embedded.html#MIPS-Embedded)
    - [21.3.7 OpenRISC 1000](OpenRISC-1000.html#OpenRISC-1000)
    - [21.3.8 PowerPC Embedded](PowerPC-Embedded.html#PowerPC-Embedded)
    - [21.3.9 Atmel AVR](AVR.html#AVR)
    - [21.3.10 CRIS](CRIS.html#CRIS)
    - [21.3.11 Renesas Super-H](Super_002dH.html#Super_002dH)
  - [21.4 Architectures](Architectures.html#Architectures)
    - [21.4.1 AArch64](AArch64.html#AArch64)
      - [21.4.1.1 AArch64 SVE.](AArch64.html#AArch64-SVE_002e)
      - [21.4.1.2 AArch64 Pointer Authentication.](AArch64.html#AArch64-Pointer-Authentication_002e)
      - [21.4.1.3 AArch64 Memory Tagging Extension.](AArch64.html#AArch64-Memory-Tagging-Extension_002e)
    - [21.4.2 x86 Architecture-specific Issues](i386.html#i386)
      - [21.4.2.1 Intel *Memory Protection Extensions* (MPX).](i386.html#Intel-Memory-Protection-Extensions-_0028MPX_0029_002e)
    - [21.4.3 Alpha](Alpha.html#Alpha)
    - [21.4.4 MIPS](MIPS.html#MIPS)
    - [21.4.5 HPPA](HPPA.html#HPPA)
    - [21.4.6 PowerPC](PowerPC.html#PowerPC)
    - [21.4.7 Nios II](Nios-II.html#Nios-II)
    - [21.4.8 Sparc64](Sparc64.html#Sparc64)
      - [21.4.8.1 ADI Support](Sparc64.html#ADI-Support)
    - [21.4.9 S12Z](S12Z.html#S12Z)
    - [21.4.10 AMD GPU](AMD-GPU.html#AMD-GPU)
      - [21.4.10.1 AMD GPU Architectures](AMD-GPU.html#AMD-GPU-Architectures)
      - [21.4.10.2 AMD GPU Device Driver and AMD ROCm Runtime](AMD-GPU.html#AMD-GPU-Device-Driver-and-AMD-ROCm-Runtime)
      - [21.4.10.3 AMD GPU Wavefronts](AMD-GPU.html#AMD-GPU-Wavefronts)
      - [21.4.10.4 AMD GPU Code Objects](AMD-GPU.html#AMD-GPU-Code-Objects)
      - [21.4.10.5 AMD GPU Entity Target Identifiers and Convenience Variables](AMD-GPU.html#AMD-GPU-Entity-Target-Identifiers-and-Convenience-Variables)
      - [21.4.10.6 AMD GPU Signals](AMD-GPU.html#AMD-GPU-Signals-1)
      - [21.4.10.7 AMD GPU Logging](AMD-GPU.html#AMD-GPU-Logging)
      - [21.4.10.8 AMD GPU Restrictions](AMD-GPU.html#AMD-GPU-Restrictions)
- [22 Controlling [GDB]
  - [22.1 Prompt](Prompt.html#Prompt)
  - [22.2 Command Editing](Editing.html#Editing)
  - [22.3 Command History](Command-History.html#Command-History)
  - [22.4 Screen Size](Screen-Size.html#Screen-Size)
  - [22.5 Output Styling](Output-Styling.html#Output-Styling)
  - [22.6 Numbers](Numbers.html#Numbers)
  - [22.7 Configuring the Current ABI](ABI.html#ABI)
  - [22.8 Automatically loading associated files](Auto_002dloading.html#Auto_002dloading)
    - [22.8.1 Automatically loading init file in the current directory](Init-File-in-the-Current-Directory.html#Init-File-in-the-Current-Directory)
    - [22.8.2 Automatically loading thread debugging library](libthread_005fdb_002eso_002e1-file.html#libthread_005fdb_002eso_002e1-file)
    - [22.8.3 Security restriction for auto-loading](Auto_002dloading-safe-path.html#Auto_002dloading-safe-path)
    - [22.8.4 Displaying files tried for auto-load](Auto_002dloading-verbose-mode.html#Auto_002dloading-verbose-mode)
  - [22.9 Optional Warnings and Messages](Messages_002fWarnings.html#Messages_002fWarnings)
  - [22.10 Optional Messages about Internal Happenings](Debugging-Output.html#Debugging-Output)
  - [22.11 Other Miscellaneous Settings](Other-Misc-Settings.html#Other-Misc-Settings)
- [23 Extending [GDB]
  - [23.1 Canned Sequences of Commands](Sequences.html#Sequences)
    - [23.1.1 User-defined Commands](Define.html#Define)
    - [23.1.2 User-defined Command Hooks](Hooks.html#Hooks)
    - [23.1.3 Command Files](Command-Files.html#Command-Files)
    - [23.1.4 Commands for Controlled Output](Output.html#Output)
    - [23.1.5 Controlling auto-loading native [GDB]
  - [23.2 Command Aliases](Aliases.html#Aliases)
    - [23.2.1 Default Arguments](Command-aliases-default-args.html#Command-aliases-default-args)
  - [23.3 Extending [GDB]
    - [23.3.1 Python Commands](Python-Commands.html#Python-Commands)
    - [23.3.2 Python API](Python-API.html#Python-API)
      - [23.3.2.1 Basic Python](Basic-Python.html#Basic-Python)
      - [23.3.2.2 Exception Handling](Exception-Handling.html#Exception-Handling)
      - [23.3.2.3 Values From Inferior](Values-From-Inferior.html#Values-From-Inferior)
      - [23.3.2.4 Types In Python](Types-In-Python.html#Types-In-Python)
      - [23.3.2.5 Pretty Printing API](Pretty-Printing-API.html#Pretty-Printing-API)
      - [23.3.2.6 Selecting Pretty-Printers](Selecting-Pretty_002dPrinters.html#Selecting-Pretty_002dPrinters)
      - [23.3.2.7 Writing a Pretty-Printer](Writing-a-Pretty_002dPrinter.html#Writing-a-Pretty_002dPrinter)
      - [23.3.2.8 Type Printing API](Type-Printing-API.html#Type-Printing-API)
      - [23.3.2.9 Filtering Frames](Frame-Filter-API.html#Frame-Filter-API)
      - [23.3.2.10 Decorating Frames](Frame-Decorator-API.html#Frame-Decorator-API)
      - [23.3.2.11 Writing a Frame Filter](Writing-a-Frame-Filter.html#Writing-a-Frame-Filter)
      - [23.3.2.12 Unwinding Frames in Python](Unwinding-Frames-in-Python.html#Unwinding-Frames-in-Python)
      - [23.3.2.13 Xmethods In Python](Xmethods-In-Python.html#Xmethods-In-Python)
      - [23.3.2.14 Xmethod API](Xmethod-API.html#Xmethod-API)
      - [23.3.2.15 Writing an Xmethod](Writing-an-Xmethod.html#Writing-an-Xmethod)
      - [23.3.2.16 Inferiors In Python](Inferiors-In-Python.html#Inferiors-In-Python)
      - [23.3.2.17 Events In Python](Events-In-Python.html#Events-In-Python)
      - [23.3.2.18 Threads In Python](Threads-In-Python.html#Threads-In-Python)
      - [23.3.2.19 Recordings In Python](Recordings-In-Python.html#Recordings-In-Python)
      - [23.3.2.20 CLI Commands In Python](CLI-Commands-In-Python.html#CLI-Commands-In-Python)
      - [23.3.2.21 [GDB/MI]
      - [23.3.2.22 Parameters In Python](Parameters-In-Python.html#Parameters-In-Python)
      - [23.3.2.23 Writing new convenience functions](Functions-In-Python.html#Functions-In-Python)
      - [23.3.2.24 Program Spaces In Python](Progspaces-In-Python.html#Progspaces-In-Python)
      - [23.3.2.25 Objfiles In Python](Objfiles-In-Python.html#Objfiles-In-Python)
      - [23.3.2.26 Accessing inferior stack frames from Python](Frames-In-Python.html#Frames-In-Python)
      - [23.3.2.27 Accessing blocks from Python](Blocks-In-Python.html#Blocks-In-Python)
      - [23.3.2.28 Python representation of Symbols](Symbols-In-Python.html#Symbols-In-Python)
      - [23.3.2.29 Symbol table representation in Python](Symbol-Tables-In-Python.html#Symbol-Tables-In-Python)
      - [23.3.2.30 Manipulating line tables using Python](Line-Tables-In-Python.html#Line-Tables-In-Python)
      - [23.3.2.31 Manipulating breakpoints using Python](Breakpoints-In-Python.html#Breakpoints-In-Python)
      - [23.3.2.32 Finish Breakpoints](Finish-Breakpoints-in-Python.html#Finish-Breakpoints-in-Python)
      - [23.3.2.33 Python representation of lazy strings](Lazy-Strings-In-Python.html#Lazy-Strings-In-Python)
      - [23.3.2.34 Python representation of architectures](Architectures-In-Python.html#Architectures-In-Python)
      - [23.3.2.35 Registers In Python](Registers-In-Python.html#Registers-In-Python)
      - [23.3.2.36 Connections In Python](Connections-In-Python.html#Connections-In-Python)
      - [23.3.2.37 Implementing new TUI windows](TUI-Windows-In-Python.html#TUI-Windows-In-Python)
      - [23.3.2.38 Instruction Disassembly In Python](Disassembly-In-Python.html#Disassembly-In-Python)
    - [23.3.3 Python Auto-loading](Python-Auto_002dloading.html#Python-Auto_002dloading)
    - [23.3.4 Python modules](Python-modules.html#Python-modules)
      - [23.3.4.1 gdb.printing](gdb_002eprinting.html#gdb_002eprinting)
      - [23.3.4.2 gdb.types](gdb_002etypes.html#gdb_002etypes)
      - [23.3.4.3 gdb.prompt](gdb_002eprompt.html#gdb_002eprompt)
  - [23.4 Extending [GDB]
    - [23.4.1 Guile Introduction](Guile-Introduction.html#Guile-Introduction)
    - [23.4.2 Guile Commands](Guile-Commands.html#Guile-Commands)
    - [23.4.3 Guile API](Guile-API.html#Guile-API)
      - [23.4.3.1 Basic Guile](Basic-Guile.html#Basic-Guile)
      - [23.4.3.2 Guile Configuration](Guile-Configuration.html#Guile-Configuration)
      - [23.4.3.3 GDB Scheme Data Types](GDB-Scheme-Data-Types.html#GDB-Scheme-Data-Types)
      - [23.4.3.4 Guile Exception Handling](Guile-Exception-Handling.html#Guile-Exception-Handling)
      - [23.4.3.5 Values From Inferior In Guile](Values-From-Inferior-In-Guile.html#Values-From-Inferior-In-Guile)
      - [23.4.3.6 Arithmetic In Guile](Arithmetic-In-Guile.html#Arithmetic-In-Guile)
      - [23.4.3.7 Types In Guile](Types-In-Guile.html#Types-In-Guile)
      - [23.4.3.8 Guile Pretty Printing API](Guile-Pretty-Printing-API.html#Guile-Pretty-Printing-API)
      - [23.4.3.9 Selecting Guile Pretty-Printers](Selecting-Guile-Pretty_002dPrinters.html#Selecting-Guile-Pretty_002dPrinters)
      - [23.4.3.10 Writing a Guile Pretty-Printer](Writing-a-Guile-Pretty_002dPrinter.html#Writing-a-Guile-Pretty_002dPrinter)
      - [23.4.3.11 Commands In Guile](Commands-In-Guile.html#Commands-In-Guile)
      - [23.4.3.12 Parameters In Guile](Parameters-In-Guile.html#Parameters-In-Guile)
      - [23.4.3.13 Program Spaces In Guile](Progspaces-In-Guile.html#Progspaces-In-Guile)
      - [23.4.3.14 Objfiles In Guile](Objfiles-In-Guile.html#Objfiles-In-Guile)
      - [23.4.3.15 Accessing inferior stack frames from Guile.](Frames-In-Guile.html#Frames-In-Guile)
      - [23.4.3.16 Accessing blocks from Guile.](Blocks-In-Guile.html#Blocks-In-Guile)
      - [23.4.3.17 Guile representation of Symbols.](Symbols-In-Guile.html#Symbols-In-Guile)
      - [23.4.3.18 Symbol table representation in Guile.](Symbol-Tables-In-Guile.html#Symbol-Tables-In-Guile)
      - [23.4.3.19 Manipulating breakpoints using Guile](Breakpoints-In-Guile.html#Breakpoints-In-Guile)
      - [23.4.3.20 Guile representation of lazy strings.](Lazy-Strings-In-Guile.html#Lazy-Strings-In-Guile)
      - [23.4.3.21 Guile representation of architectures](Architectures-In-Guile.html#Architectures-In-Guile)
      - [23.4.3.22 Disassembly In Guile](Disassembly-In-Guile.html#Disassembly-In-Guile)
      - [23.4.3.23 I/O Ports in Guile](I_002fO-Ports-in-Guile.html#I_002fO-Ports-in-Guile)
      - [23.4.3.24 Memory Ports in Guile](Memory-Ports-in-Guile.html#Memory-Ports-in-Guile)
      - [23.4.3.25 Iterators In Guile](Iterators-In-Guile.html#Iterators-In-Guile)
    - [23.4.4 Guile Auto-loading](Guile-Auto_002dloading.html#Guile-Auto_002dloading)
    - [23.4.5 Guile Modules](Guile-Modules.html#Guile-Modules)
      - [23.4.5.1 Guile Printing Module](Guile-Printing-Module.html#Guile-Printing-Module)
      - [23.4.5.2 Guile Types Module](Guile-Types-Module.html#Guile-Types-Module)
  - [23.5 Auto-loading extensions](Auto_002dloading-extensions.html#Auto_002dloading-extensions)
    - [23.5.1 The `objfile-gdb.ext`
    - [23.5.2 The `.debug_gdb_scripts` section](dotdebug_005fgdb_005fscripts-section.html#dotdebug_005fgdb_005fscripts-section)
      - [23.5.2.1 Script File Entries](dotdebug_005fgdb_005fscripts-section.html#Script-File-Entries)
      - [23.5.2.2 Script Text Entries](dotdebug_005fgdb_005fscripts-section.html#Script-Text-Entries)
    - [23.5.3 Which flavor to choose?](Which-flavor-to-choose_003f.html#Which-flavor-to-choose_003f)
  - [23.6 Multiple Extension Languages](Multiple-Extension-Languages.html#Multiple-Extension-Languages)
    - [23.6.1 Python comes first](Multiple-Extension-Languages.html#Python-comes-first)
- [24 Command Interpreters](Interpreters.html#Interpreters)
- [25 [GDB]
  - [25.1 TUI Overview](TUI-Overview.html#TUI-Overview)
  - [25.2 TUI Key Bindings](TUI-Keys.html#TUI-Keys)
  - [25.3 TUI Single Key Mode](TUI-Single-Key-Mode.html#TUI-Single-Key-Mode)
  - [25.4 TUI Mouse Support](TUI-Mouse-Support.html#TUI-Mouse-Support)
  - [25.5 TUI-specific Commands](TUI-Commands.html#TUI-Commands)
  - [25.6 TUI Configuration Variables](TUI-Configuration.html#TUI-Configuration)
- [26 Using [GDB]
- [27 The [GDB/MI]
  - [Function and Purpose](GDB_002fMI.html#Function-and-Purpose)
  - [Notation and Terminology](GDB_002fMI.html#Notation-and-Terminology)
  - [27.1 [GDB/MI]
    - [27.1.1 Context management](Context-management.html#Context-management)
      - [27.1.1.1 Threads and Frames](Context-management.html#Threads-and-Frames)
      - [27.1.1.2 Language](Context-management.html#Language)
    - [27.1.2 Asynchronous command execution and non-stop mode](Asynchronous-and-non_002dstop-modes.html#Asynchronous-and-non_002dstop-modes)
    - [27.1.3 Thread groups](Thread-groups.html#Thread-groups)
  - [27.2 [GDB/MI]
    - [27.2.1 [GDB/MI]
    - [27.2.2 [GDB/MI]
  - [27.3 [GDB/MI]
  - [27.4 [GDB/MI]
  - [27.5 [GDB/MI]
    - [27.5.1 [GDB/MI]
    - [27.5.2 [GDB/MI]
    - [27.5.3 [GDB/MI]
    - [27.5.4 [GDB/MI]
    - [27.5.5 [GDB/MI]
    - [27.5.6 [GDB/MI]
    - [27.5.7 [GDB/MI]
  - [27.6 Simple Examples of [GDB/MI]
  - [27.7 [GDB/MI]
  - [27.8 [GDB/MI]
  - [27.9 [GDB/MI]
    - [27.9.1 Shared Library [GDB/MI]
    - [27.9.2 Ada Exception [GDB/MI]
    - [27.9.3 C++ Exception [GDB/MI]
  - [27.10 [GDB/MI]
  - [27.11 [GDB/MI]
  - [27.12 [GDB/MI]
  - [27.13 [GDB/MI]
  - [27.14 [GDB/MI]
  - [27.15 [GDB/MI]
  - [27.16 [GDB/MI]
  - [27.17 [GDB/MI]
  - [27.18 [GDB/MI]
  - [27.19 [GDB/MI]
  - [27.20 [GDB/MI]
  - [27.21 [GDB/MI]
  - [27.22 Ada Exceptions [GDB/MI]
  - [27.23 [GDB/MI]
  - [27.24 Miscellaneous [GDB/MI]
- [28 [GDB]
  - [28.1 What is an Annotation?](Annotations-Overview.html#Annotations-Overview)
  - [28.2 The Server Prefix](Server-Prefix.html#Server-Prefix)
  - [28.3 Annotation for [GDB]
  - [28.4 Errors](Errors.html#Errors)
  - [28.5 Invalidation Notices](Invalidation.html#Invalidation)
  - [28.6 Running the Program](Annotations-for-Running.html#Annotations-for-Running)
  - [28.7 Displaying Source](Source-Annotations.html#Source-Annotations)
- [29 Debugger Adapter Protocol](Debugger-Adapter-Protocol.html#Debugger-Adapter-Protocol)
- [30 JIT Compilation Interface](JIT-Interface.html#JIT-Interface)
  - [30.1 JIT Declarations](Declarations.html#Declarations)
  - [30.2 Registering Code](Registering-Code.html#Registering-Code)
  - [30.3 Unregistering Code](Unregistering-Code.html#Unregistering-Code)
  - [30.4 Custom Debug Info](Custom-Debug-Info.html#Custom-Debug-Info)
    - [30.4.1 Using JIT Debug Info Readers](Using-JIT-Debug-Info-Readers.html#Using-JIT-Debug-Info-Readers)
    - [30.4.2 Writing JIT Debug Info Readers](Writing-JIT-Debug-Info-Readers.html#Writing-JIT-Debug-Info-Readers)
- [31 In-Process Agent](In_002dProcess-Agent.html#In_002dProcess-Agent)
  - [31.1 In-Process Agent Protocol](In_002dProcess-Agent-Protocol.html#In_002dProcess-Agent-Protocol)
    - [31.1.1 IPA Protocol Objects](IPA-Protocol-Objects.html#IPA-Protocol-Objects)
    - [31.1.2 IPA Protocol Commands](IPA-Protocol-Commands.html#IPA-Protocol-Commands)
- [32 Reporting Bugs in [GDB]
  - [32.1 Have You Found a Bug?](Bug-Criteria.html#Bug-Criteria)
  - [32.2 How to Report Bugs](Bug-Reporting.html#Bug-Reporting)
- [33 Command Line Editing](Command-Line-Editing.html#Command-Line-Editing)
  - [33.1 Introduction to Line Editing](Introduction-and-Notation.html#Introduction-and-Notation)
  - [33.2 Readline Interaction](Readline-Interaction.html#Readline-Interaction)
    - [33.2.1 Readline Bare Essentials](Readline-Bare-Essentials.html#Readline-Bare-Essentials)
    - [33.2.2 Readline Movement Commands](Readline-Movement-Commands.html#Readline-Movement-Commands)
    - [33.2.3 Readline Killing Commands](Readline-Killing-Commands.html#Readline-Killing-Commands)
    - [33.2.4 Readline Arguments](Readline-Arguments.html#Readline-Arguments)
    - [33.2.5 Searching for Commands in the History](Searching.html#Searching)
  - [33.3 Readline Init File](Readline-Init-File.html#Readline-Init-File)
    - [33.3.1 Readline Init File Syntax](Readline-Init-File-Syntax.html#Readline-Init-File-Syntax)
    - [33.3.2 Conditional Init Constructs](Conditional-Init-Constructs.html#Conditional-Init-Constructs)
    - [33.3.3 Sample Init File](Sample-Init-File.html#Sample-Init-File)
  - [33.4 Bindable Readline Commands](Bindable-Readline-Commands.html#Bindable-Readline-Commands)
    - [33.4.1 Commands For Moving](Commands-For-Moving.html#Commands-For-Moving)
    - [33.4.2 Commands For Manipulating The History](Commands-For-History.html#Commands-For-History)
    - [33.4.3 Commands For Changing Text](Commands-For-Text.html#Commands-For-Text)
    - [33.4.4 Killing And Yanking](Commands-For-Killing.html#Commands-For-Killing)
    - [33.4.5 Specifying Numeric Arguments](Numeric-Arguments.html#Numeric-Arguments)
    - [33.4.6 Letting Readline Type For You](Commands-For-Completion.html#Commands-For-Completion)
    - [33.4.7 Keyboard Macros](Keyboard-Macros.html#Keyboard-Macros)
    - [33.4.8 Some Miscellaneous Commands](Miscellaneous-Commands.html#Miscellaneous-Commands)
  - [33.5 Readline vi Mode](Readline-vi-Mode.html#Readline-vi-Mode)
- [34 Using History Interactively](Using-History-Interactively.html#Using-History-Interactively)
  - [34.1 History Expansion](History-Interaction.html#History-Interaction)
    - [34.1.1 Event Designators](Event-Designators.html#Event-Designators)
    - [34.1.2 Word Designators](Word-Designators.html#Word-Designators)
    - [34.1.3 Modifiers](Modifiers.html#Modifiers)
- [Appendix A In Memoriam](In-Memoriam.html#In-Memoriam)
- [Appendix B Formatting Documentation](Formatting-Documentation.html#Formatting-Documentation)
- [Appendix C Installing [GDB]
  - [C.1 Requirements for Building [GDB]
  - [C.2 Invoking the [GDB]
  - [C.3 Compiling [GDB]
  - [C.4 Specifying Names for Hosts and Targets](Config-Names.html#Config-Names)
  - [C.5 `configure`
  - [C.6 System-wide configuration and settings](System_002dwide-configuration.html#System_002dwide-configuration)
    - [C.6.1 Installed System-wide Configuration Scripts](System_002dwide-Configuration-Scripts.html#System_002dwide-Configuration-Scripts)
- [Appendix D Maintenance Commands](Maintenance-Commands.html#Maintenance-Commands)
- [Appendix E [GDB]
  - [E.1 Overview](Overview.html#Overview)
  - [E.2 Packets](Packets.html#Packets)
  - [E.3 Stop Reply Packets](Stop-Reply-Packets.html#Stop-Reply-Packets)
  - [E.4 General Query Packets](General-Query-Packets.html#General-Query-Packets)
  - [E.5 Architecture-Specific Protocol Details](Architecture_002dSpecific-Protocol-Details.html#Architecture_002dSpecific-Protocol-Details)
    - [E.5.1 ARM-specific Protocol Details](ARM_002dSpecific-Protocol-Details.html#ARM_002dSpecific-Protocol-Details)
      - [E.5.1.1 ARM Breakpoint Kinds](ARM-Breakpoint-Kinds.html#ARM-Breakpoint-Kinds)
      - [E.5.1.2 ARM Memory Tag Types](ARM-Memory-Tag-Types.html#ARM-Memory-Tag-Types)
    - [E.5.2 MIPS-specific Protocol Details](MIPS_002dSpecific-Protocol-Details.html#MIPS_002dSpecific-Protocol-Details)
      - [E.5.2.1 MIPS Register Packet Format](MIPS-Register-packet-Format.html#MIPS-Register-packet-Format)
      - [E.5.2.2 MIPS Breakpoint Kinds](MIPS-Breakpoint-Kinds.html#MIPS-Breakpoint-Kinds)
  - [E.6 Tracepoint Packets](Tracepoint-Packets.html#Tracepoint-Packets)
    - [E.6.1 Relocate instruction reply packet](Tracepoint-Packets.html#Relocate-instruction-reply-packet)
  - [E.7 Host I/O Packets](Host-I_002fO-Packets.html#Host-I_002fO-Packets)
  - [E.8 Interrupts](Interrupts.html#Interrupts)
  - [E.9 Notification Packets](Notification-Packets.html#Notification-Packets)
  - [E.10 Remote Protocol Support for Non-Stop Mode](Remote-Non_002dStop.html#Remote-Non_002dStop)
  - [E.11 Packet Acknowledgment](Packet-Acknowledgment.html#Packet-Acknowledgment)
  - [E.12 Examples](Examples.html#Examples)
  - [E.13 File-I/O Remote Protocol Extension](File_002dI_002fO-Remote-Protocol-Extension.html#File_002dI_002fO-Remote-Protocol-Extension)
    - [E.13.1 File-I/O Overview](File_002dI_002fO-Overview.html#File_002dI_002fO-Overview)
    - [E.13.2 Protocol Basics](Protocol-Basics.html#Protocol-Basics)
    - [E.13.3 The `F` Request Packet](The-F-Request-Packet.html#The-F-Request-Packet)
    - [E.13.4 The `F` Reply Packet](The-F-Reply-Packet.html#The-F-Reply-Packet)
    - [E.13.5 The '`Ctrl-C`
    - [E.13.6 Console I/O](Console-I_002fO.html#Console-I_002fO)
    - [E.13.7 List of Supported Calls](List-of-Supported-Calls.html#List-of-Supported-Calls)
      - [open](open.html#open)
      - [close](close.html#close)
      - [read](read.html#read)
      - [write](write.html#write)
      - [lseek](lseek.html#lseek)
      - [rename](rename.html#rename)
      - [unlink](unlink.html#unlink)
      - [stat/fstat](stat_002ffstat.html#stat_002ffstat)
      - [gettimeofday](gettimeofday.html#gettimeofday)
      - [isatty](isatty.html#isatty)
      - [system](system.html#system)
    - [E.13.8 Protocol-specific Representation of Datatypes](Protocol_002dspecific-Representation-of-Datatypes.html#Protocol_002dspecific-Representation-of-Datatypes)
      - [Integral Datatypes](Integral-Datatypes.html#Integral-Datatypes)
      - [Pointer Values](Pointer-Values.html#Pointer-Values)
      - [Memory Transfer](Memory-Transfer.html#Memory-Transfer)
      - [struct stat](struct-stat.html#struct-stat)
      - [struct timeval](struct-timeval.html#struct-timeval)
    - [E.13.9 Constants](Constants.html#Constants)
      - [Open Flags](Open-Flags.html#Open-Flags)
      - [mode_t Values](mode_005ft-Values.html#mode_005ft-Values)
      - [Errno Values](Errno-Values.html#Errno-Values)
      - [Lseek Flags](Lseek-Flags.html#Lseek-Flags)
      - [Limits](Limits.html#Limits)
    - [E.13.10 File-I/O Examples](File_002dI_002fO-Examples.html#File_002dI_002fO-Examples)
  - [E.14 Library List Format](Library-List-Format.html#Library-List-Format)
  - [E.15 Library List Format for SVR4 Targets](Library-List-Format-for-SVR4-Targets.html#Library-List-Format-for-SVR4-Targets)
  - [E.16 Memory Map Format](Memory-Map-Format.html#Memory-Map-Format)
  - [E.17 Thread List Format](Thread-List-Format.html#Thread-List-Format)
  - [E.18 Traceframe Info Format](Traceframe-Info-Format.html#Traceframe-Info-Format)
  - [E.19 Branch Trace Format](Branch-Trace-Format.html#Branch-Trace-Format)
  - [E.20 Branch Trace Configuration Format](Branch-Trace-Configuration-Format.html#Branch-Trace-Configuration-Format)
- [Appendix F The GDB Agent Expression Mechanism](Agent-Expressions.html#Agent-Expressions)
  - [F.1 General Bytecode Design](General-Bytecode-Design.html#General-Bytecode-Design)
  - [F.2 Bytecode Descriptions](Bytecode-Descriptions.html#Bytecode-Descriptions)
  - [F.3 Using Agent Expressions](Using-Agent-Expressions.html#Using-Agent-Expressions)
  - [F.4 Varying Target Capabilities](Varying-Target-Capabilities.html#Varying-Target-Capabilities)
  - [F.5 Rationale](Rationale.html#Rationale)
- [Appendix G Target Descriptions](Target-Descriptions.html#Target-Descriptions)
  - [G.1 Retrieving Descriptions](Retrieving-Descriptions.html#Retrieving-Descriptions)
  - [G.2 Target Description Format](Target-Description-Format.html#Target-Description-Format)
    - [G.2.1 Inclusion](Target-Description-Format.html#Inclusion)
    - [G.2.2 Architecture](Target-Description-Format.html#Architecture)
    - [G.2.3 OS ABI](Target-Description-Format.html#OS-ABI)
    - [G.2.4 Compatible Architecture](Target-Description-Format.html#Compatible-Architecture)
    - [G.2.5 Features](Target-Description-Format.html#Features)
    - [G.2.6 Types](Target-Description-Format.html#Types)
    - [G.2.7 Registers](Target-Description-Format.html#Registers-2)
  - [G.3 Predefined Target Types](Predefined-Target-Types.html#Predefined-Target-Types)
  - [G.4 Enum Target Types](Enum-Target-Types.html#Enum-Target-Types)
  - [G.5 Standard Target Features](Standard-Target-Features.html#Standard-Target-Features)
    - [G.5.1 AArch64 Features](AArch64-Features.html#AArch64-Features)
      - [G.5.1.1 AArch64 core registers feature](AArch64-Features.html#AArch64-core-registers-feature)
      - [G.5.1.2 AArch64 floating-point registers feature](AArch64-Features.html#AArch64-floating_002dpoint-registers-feature)
      - [G.5.1.3 AArch64 SVE registers feature](AArch64-Features.html#AArch64-SVE-registers-feature)
      - [G.5.1.4 AArch64 Pointer Authentication registers feature](AArch64-Features.html#AArch64-Pointer-Authentication-registers-feature)
      - [G.5.1.5 AArch64 TLS registers feature](AArch64-Features.html#AArch64-TLS-registers-feature)
      - [G.5.1.6 AArch64 MTE registers feature](AArch64-Features.html#AArch64-MTE-registers-feature)
    - [G.5.2 ARC Features](ARC-Features.html#ARC-Features)
    - [G.5.3 ARM Features](ARM-Features.html#ARM-Features)
      - [G.5.3.1 Core register set for non-M-profile](ARM-Features.html#Core-register-set-for-non_002dM_002dprofile)
      - [G.5.3.2 Core register set for M-profile](ARM-Features.html#Core-register-set-for-M_002dprofile)
      - [G.5.3.3 FPA registers feature (obsolete)](ARM-Features.html#FPA-registers-feature-_0028obsolete_0029)
      - [G.5.3.4 M-profile Vector Extension (MVE)](ARM-Features.html#M_002dprofile-Vector-Extension-_0028MVE_0029)
      - [G.5.3.5 XScale iwMMXt feature](ARM-Features.html#XScale-iwMMXt-feature)
      - [G.5.3.6 Vector Floating-Point (VFP) feature](ARM-Features.html#Vector-Floating_002dPoint-_0028VFP_0029-feature)
      - [G.5.3.7 NEON architecture feature](ARM-Features.html#NEON-architecture-feature)
      - [G.5.3.8 M-profile Pointer Authentication and Branch Target Identification feature](ARM-Features.html#M_002dprofile-Pointer-Authentication-and-Branch-Target-Identification-feature)
      - [G.5.3.9 M-profile system registers feature](ARM-Features.html#M_002dprofile-system-registers-feature)
      - [G.5.3.10 M-profile Security Extensions feature](ARM-Features.html#M_002dprofile-Security-Extensions-feature)
      - [G.5.3.11 TLS registers feature](ARM-Features.html#TLS-registers-feature)
    - [G.5.4 i386 Features](i386-Features.html#i386-Features)
    - [G.5.5 LoongArch Features](LoongArch-Features.html#LoongArch-Features)
    - [G.5.6 MicroBlaze Features](MicroBlaze-Features.html#MicroBlaze-Features)
    - [G.5.7 MIPS Features](MIPS-Features.html#MIPS-Features)
    - [G.5.8 M68K Features](M68K-Features.html#M68K-Features)
    - [G.5.9 NDS32 Features](NDS32-Features.html#NDS32-Features)
    - [G.5.10 Nios II Features](Nios-II-Features.html#Nios-II-Features)
    - [G.5.11 Openrisc 1000 Features](OpenRISC-1000-Features.html#OpenRISC-1000-Features)
    - [G.5.12 PowerPC Features](PowerPC-Features.html#PowerPC-Features)
    - [G.5.13 RISC-V Features](RISC_002dV-Features.html#RISC_002dV-Features)
    - [G.5.14 RX Features](RX-Features.html#RX-Features)
    - [G.5.15 S/390 and System z Features](S_002f390-and-System-z-Features.html#S_002f390-and-System-z-Features)
    - [G.5.16 Sparc Features](Sparc-Features.html#Sparc-Features)
    - [G.5.17 TMS320C6x Features](TIC6x-Features.html#TIC6x-Features)
- [Appendix H Operating System Information](Operating-System-Information.html#Operating-System-Information)
  - [H.1 Process list](Process-list.html#Process-list)
- [Appendix I Trace File Format](Trace-File-Format.html#Trace-File-Format)
- [Appendix J `.gdb_index` section format](Index-Section-Format.html#Index-Section-Format)
- [Appendix K Download debugging resources with Debuginfod](Debuginfod.html#Debuginfod)
  - [K.1 Debuginfod Settings](Debuginfod-Settings.html#Debuginfod-Settings)
- [Appendix L Manual pages](Man-Pages.html#Man-Pages)
- [Appendix M GNU GENERAL PUBLIC LICENSE](Copying.html#Copying)
- [Appendix N GNU Free Documentation License](GNU-Free-Documentation-License.html#GNU-Free-Documentation-License)
- [Concept Index](Concept-Index.html#Concept-Index)
- [Command, Variable, and Function Index](Command-and-Variable-Index.html#Command-and-Variable-Index)
  :::

---

::: header
Next: [Summary](Summary.html#Summary)]
:::
