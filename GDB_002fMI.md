---
description: GDB/MI (Debugging with GDB)
distribution: global
Generator: makeinfo
keywords: GDB/MI (Debugging with GDB)
lang: en
resource-type: document
title: GDB/MI (Debugging with GDB)
---
::: header
Next: [Annotations](Annotations.html#Annotations)]
:::

---

## 27 The [GDB/MI]

---

• [GDB/MI General Design](GDB_002fMI-General-Design.html#GDB_002fMI-General-Design):                                         
• [GDB/MI Command Syntax](GDB_002fMI-Command-Syntax.html#GDB_002fMI-Command-Syntax):                                         
• [GDB/MI Compatibility with CLI](GDB_002fMI-Compatibility-with-CLI.html#GDB_002fMI-Compatibility-with-CLI):                 
• [GDB/MI Development and Front Ends](GDB_002fMI-Development-and-Front-Ends.html#GDB_002fMI-Development-and-Front-Ends):     
• [GDB/MI Output Records](GDB_002fMI-Output-Records.html#GDB_002fMI-Output-Records):                                         
• [GDB/MI Simple Examples](GDB_002fMI-Simple-Examples.html#GDB_002fMI-Simple-Examples):                                      
• [GDB/MI Command Description Format](GDB_002fMI-Command-Description-Format.html#GDB_002fMI-Command-Description-Format):     
• [GDB/MI Breakpoint Commands](GDB_002fMI-Breakpoint-Commands.html#GDB_002fMI-Breakpoint-Commands):                          
• [GDB/MI Catchpoint Commands](GDB_002fMI-Catchpoint-Commands.html#GDB_002fMI-Catchpoint-Commands):                          
• [GDB/MI Program Context](GDB_002fMI-Program-Context.html#GDB_002fMI-Program-Context):                                                     
• [GDB/MI Thread Commands](GDB_002fMI-Thread-Commands.html#GDB_002fMI-Thread-Commands):                                                     
• [GDB/MI Ada Tasking Commands](GDB_002fMI-Ada-Tasking-Commands.html#GDB_002fMI-Ada-Tasking-Commands):                                      
• [GDB/MI Program Execution](GDB_002fMI-Program-Execution.html#GDB_002fMI-Program-Execution):                                               
• [GDB/MI Stack Manipulation](GDB_002fMI-Stack-Manipulation.html#GDB_002fMI-Stack-Manipulation):                                            
• [GDB/MI Variable Objects](GDB_002fMI-Variable-Objects.html#GDB_002fMI-Variable-Objects):                                                  
• [GDB/MI Data Manipulation](GDB_002fMI-Data-Manipulation.html#GDB_002fMI-Data-Manipulation):                                               
• [GDB/MI Tracepoint Commands](GDB_002fMI-Tracepoint-Commands.html#GDB_002fMI-Tracepoint-Commands):                                         
• [GDB/MI Symbol Query](GDB_002fMI-Symbol-Query.html#GDB_002fMI-Symbol-Query):                                                              
• [GDB/MI File Commands](GDB_002fMI-File-Commands.html#GDB_002fMI-File-Commands):                                                           
• [GDB/MI Target Manipulation](GDB_002fMI-Target-Manipulation.html#GDB_002fMI-Target-Manipulation):                                         
• [GDB/MI File Transfer Commands](GDB_002fMI-File-Transfer-Commands.html#GDB_002fMI-File-Transfer-Commands):                                
• [GDB/MI Ada Exceptions Commands](GDB_002fMI-Ada-Exceptions-Commands.html#GDB_002fMI-Ada-Exceptions-Commands):                             
• [GDB/MI Support Commands](GDB_002fMI-Support-Commands.html#GDB_002fMI-Support-Commands):                                                  
• [GDB/MI Miscellaneous Commands](GDB_002fMI-Miscellaneous-Commands.html#GDB_002fMI-Miscellaneous-Commands):                                

---

### Function and Purpose

[GDB/MI] command line option (see [Mode Options](Mode-Options.html#Mode-Options)). It is specifically intended to support the development of systems which use the debugger as just one small component of a larger system.

This chapter is a specification of the [GDB/MI] interface. It is written in the form of a reference manual.

Note that [GDB/MI] Development and Front Ends](GDB_002fMI-Development-and-Front-Ends.html#GDB_002fMI-Development-and-Front-Ends)).

### Notation and Terminology

This chapter uses the following notation:

- `|` separates two alternatives.
- `[ something ]` indicates that `something` is optional: it may or may not be given.
- `( group )*` means that `group` inside the parentheses may repeat zero or more times.
- `( group )+` means that `group` inside the parentheses may repeat one or more times.
- `( group )` means that `group` inside the parentheses occurs exactly once.
- `"string"` means a literal `string`.

---

• [GDB/MI General Design](GDB_002fMI-General-Design.html#GDB_002fMI-General-Design):                                         
• [GDB/MI Command Syntax](GDB_002fMI-Command-Syntax.html#GDB_002fMI-Command-Syntax):                                         
• [GDB/MI Compatibility with CLI](GDB_002fMI-Compatibility-with-CLI.html#GDB_002fMI-Compatibility-with-CLI):                 
• [GDB/MI Development and Front Ends](GDB_002fMI-Development-and-Front-Ends.html#GDB_002fMI-Development-and-Front-Ends):     
• [GDB/MI Output Records](GDB_002fMI-Output-Records.html#GDB_002fMI-Output-Records):                                         
• [GDB/MI Simple Examples](GDB_002fMI-Simple-Examples.html#GDB_002fMI-Simple-Examples):                                      
• [GDB/MI Command Description Format](GDB_002fMI-Command-Description-Format.html#GDB_002fMI-Command-Description-Format):     
• [GDB/MI Breakpoint Commands](GDB_002fMI-Breakpoint-Commands.html#GDB_002fMI-Breakpoint-Commands):                          
• [GDB/MI Catchpoint Commands](GDB_002fMI-Catchpoint-Commands.html#GDB_002fMI-Catchpoint-Commands):                          
• [GDB/MI Program Context](GDB_002fMI-Program-Context.html#GDB_002fMI-Program-Context):                                                     
• [GDB/MI Thread Commands](GDB_002fMI-Thread-Commands.html#GDB_002fMI-Thread-Commands):                                                     
• [GDB/MI Ada Tasking Commands](GDB_002fMI-Ada-Tasking-Commands.html#GDB_002fMI-Ada-Tasking-Commands):                                      
• [GDB/MI Program Execution](GDB_002fMI-Program-Execution.html#GDB_002fMI-Program-Execution):                                               
• [GDB/MI Stack Manipulation](GDB_002fMI-Stack-Manipulation.html#GDB_002fMI-Stack-Manipulation):                                            
• [GDB/MI Variable Objects](GDB_002fMI-Variable-Objects.html#GDB_002fMI-Variable-Objects):                                                  
• [GDB/MI Data Manipulation](GDB_002fMI-Data-Manipulation.html#GDB_002fMI-Data-Manipulation):                                               
• [GDB/MI Tracepoint Commands](GDB_002fMI-Tracepoint-Commands.html#GDB_002fMI-Tracepoint-Commands):                                         
• [GDB/MI Symbol Query](GDB_002fMI-Symbol-Query.html#GDB_002fMI-Symbol-Query):                                                              
• [GDB/MI File Commands](GDB_002fMI-File-Commands.html#GDB_002fMI-File-Commands):                                                           
• [GDB/MI Target Manipulation](GDB_002fMI-Target-Manipulation.html#GDB_002fMI-Target-Manipulation):                                         
• [GDB/MI File Transfer Commands](GDB_002fMI-File-Transfer-Commands.html#GDB_002fMI-File-Transfer-Commands):                                
• [GDB/MI Ada Exceptions Commands](GDB_002fMI-Ada-Exceptions-Commands.html#GDB_002fMI-Ada-Exceptions-Commands):                             
• [GDB/MI Support Commands](GDB_002fMI-Support-Commands.html#GDB_002fMI-Support-Commands):                                                  
• [GDB/MI Miscellaneous Commands](GDB_002fMI-Miscellaneous-Commands.html#GDB_002fMI-Miscellaneous-Commands):                                

---

---

::: header
Next: [Annotations](Annotations.html#Annotations)]
:::
