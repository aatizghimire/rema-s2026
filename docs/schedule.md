## DETAILED WEEK-BY-WEEK SYLLABUS

Here you will find the detailed weekly schedule and themes of the course. This proposed schedule is indicative and may be refined based on instructional needs and pacing.

### Week 1: Foundations – Debugging & Lab Environment

#### Workshop 1.1: RE Track – x64dbg Debugger for Beginners
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **1.1 Introduction to Debugging** | What is a debugger? Uses in RE and malware analysis; x64dbg vs OllyDbg vs IDA Pro; Installation and initial setup |
| **1.2 x64dbg Interface** | CPU view (Disassembly, Registers, Stack, Memory dump); Breakpoints tab; Symbols tab; Comments and labels |
| **1.3 Breakpoints** | Software breakpoints (INT3); Hardware breakpoints (DR0-DR3); Memory breakpoints; Conditional breakpoints |
| **1.4 Stepping Through Code** | Step Into (F7); Step Over (F8); Run to Selection (F4); Run (F9); Restart (Ctrl+F2) |
| **1.5 Patching Binaries** | Modifying instructions; Replacing jumps with NOPs; Saving patched executables |

* **Lab Exercise:** Load a CrackMe, set breakpoint on `strcmp`, modify EAX register, patch the binary to force success.
* **Homework:** Solve CrackMe2.exe independently; write a paragraph explaining the patch.

#### Workshop 1.2: MA Track – Lab Setup & OS Fundamentals
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **1.1 Virtualization for Malware Analysis** | Why VMs are essential; Isolation and snapshots; Oracle VirtualBox vs VMware; Networking modes (NAT, Host-Only, Bridged) |
| **1.2 Flare-VM Installation** | What is Flare-VM? Tools included; Installation script walkthrough; Post-installation verification |
| **1.3 Windows OS Fundamentals** | Processes vs Threads; Handles and objects; User mode vs Kernel mode; Privilege levels (Ring 0 vs Ring 3) |
| **1.4 Virtual Memory** | Physical vs Virtual addresses; Page tables; Memory protection (Read, Write, Execute); Address space layout |
| **1.5 Safe Analysis Practices** | Never run malware on host; Snapshot before each analysis; Network isolation; Reverting after analysis |

* **Lab Exercise:** Install VirtualBox + Windows 10 + Flare-VM; take a "Clean Base" snapshot; explore the Reverse Engineering folder.
* **Homework:** Take a screenshot of Flare-VM desktop with x64dbg open; read "Malware Analysis: The Safe Way" handout.

---

### Week 2: GUI Programs & PE Structure

#### Workshop 2.1: RE Track – Windows GUI Programs
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **2.1 GUI vs Console Programs** | Event-driven programming; Message loop; Common GUI controls (buttons, text boxes, dialogs) |
| **2.2 Common GUI APIs** | `MessageBox`, `GetDlgItemText`, `GetWindowText`, `EnableWindow`, `SendMessage` |
| **2.3 Conditional Jumps** | JZ (Jump if Zero); JNZ (Jump if Not Zero); JE (Jump if Equal); JNE (Jump if Not Equal); JG/JL (Signed comparisons) |
| **2.4 The NOP Instruction** | Opcode 0x90; Uses for removing instructions; Patching out function calls |
| **2.5 Removing Nag Screens** | Locating `MessageBox` calls; Replacing with NOPs or JMPs; Verifying removal |
| **2.6 Bypassing Trial Periods** | Finding timer/date checks; Modifying EAX to return "registered" value; Hardware breakpoints on system time APIs |

* **Lab Exercise:** Remove nag screen from NagScreen.exe; bypass trial expiration in Trial.exe using hardware breakpoints.
* **Homework:** Solve Registration.exe (find serial or patch); document the critical jump address.

#### Workshop 2.2: MA Track – PE File Structure & Static Analysis
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **2.1 PE File Format** | DOS header (MZ signature); DOS stub; NT headers (Signature, File Header, Optional Header); Section headers |
| **2.2 PE Sections** | `.text` (executable code); `.data` (initialized data); `.rdata` (read-only data, imports); `.rsrc` (resources); `.reloc` (relocations) |
| **2.3 The Import Address Table (IAT)** | What is the IAT? How APIs are resolved; Imported functions as indicators |
| **2.4 Packing Introduction** | Why malware packs; Compression vs encryption; OEP (Original Entry Point) hiding |
| **2.5 Identifying Packers** | Detect It Easy (DiE) tool; Packer signatures; UPX, ASPack, MPRESS, PECompact |
| **2.6 Static Analysis Tools** | PE-Bear (view PE structure); CFF Explorer (advanced PE editing); Strings (extract ASCII/Unicode); Hashing (MD5, SHA1) |
| **2.7 Entropy Analysis** | High entropy indicates packing/encryption; Calculating entropy in PE-Bear |

* **Lab Exercise:** Analyze notepad.exe vs packed sample in PE-Bear; identify packer with DiE; run strings on both; compare entropy.
* **Homework:** Statically analyze Sample2_unknown.exe – is it packed? What packer? Suspicious imports? Write 1-page report.

---

### Week 3: Assembly Language Refresher

#### Workshop 3.1: RE Track – Assembly Registers, Stack, & Jumps
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **3.1 x86 Register Set** | EAX (accumulator); EBX (base); ECX (counter); EDX (data); ESI (source index); EDI (destination index); EBP (base pointer); ESP (stack pointer); EIP (instruction pointer) |
| **3.2 General Purpose Registers** | Usage conventions; Which registers are preserved across calls? |
| **3.3 The Stack** | Stack growth direction; PUSH instruction; POP instruction; How ESP changes |
| **3.4 Function Prologue/Epilogue** | PUSH EBP; MOV EBP, ESP; LEAVE; RET; Stack frames |
| **3.5 CALL and RET** | How CALL pushes return address; How RET pops it; Nested calls |
| **3.6 Common Instructions** | MOV, ADD, SUB, INC, DEC, CMP, TEST, XOR, AND, OR |

* **Lab Exercise:** Load simple C program into x64dbg; step through each instruction; watch registers and stack change; trace a function call.
* **Homework:** Complete assembly worksheet (10 questions covering registers, stack, and instructions).

#### Workshop 3.2: MA Track – Malicious APIs & API Tracing
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **3.1 Malware API Categories** | Memory manipulation; Process injection; Persistence; Network communication; Anti-debug/anti-VM |
| **3.2 Memory APIs** | `VirtualAlloc` (allocate memory); `VirtualProtect` (change protection); `VirtualFree` (free memory) |
| **3.3 Process Injection APIs** | `OpenProcess` (get handle); `WriteProcessMemory` (write to remote); `CreateRemoteThread` (execute in remote); `QueueUserAPC` (APC injection) |
| **3.4 Persistence APIs** | `RegCreateKeyEx` / `RegSetValueEx` (Run keys); `CreateService` (Windows services); `Schtasks` (scheduled tasks) |
| **3.5 Network APIs** | `InternetOpen` / `InternetConnect` (WinINet); `HttpSendRequest` (HTTP); `WSASocket` (raw sockets) |
| **3.6 Calling Conventions** | `__stdcall` (Windows API standard); `__cdecl` (C default); `__fastcall` (fastcall); Parameter passing on stack |
| **3.7 Tracing APIs in x64dbg** | Setting breakpoints on APIs; Inspecting stack parameters; Understanding return values |

* **Lab Exercise:** Load malware sample into x64dbg; set breakpoints on `VirtualAlloc` and `CreateRemoteThread`; inspect parameters on stack.
* **Homework:** Trace Sample3.exe – list all malicious APIs called in order with their arguments.

---

### Week 4: Graphical Static Analysis & Dynamic Analysis

#### Workshop 4.1: RE Track – x64dbg Graphical Static Analysis
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **4.1 Static vs Dynamic Analysis** | Differences; When to use each; Combining both in x64dbg |
| **4.2 Graphical (Flowchart) View** | Enabling Graph view; Basic blocks; Conditional edges; Red (not taken) vs Green (taken) paths |
| **4.3 Navigation in Graph View** | Zooming; Panning; Click to jump to block; Finding loops and branches |
| **4.4 Identifying Code Paths** | Locating the "good" path; Locating the "bad" path; Understanding control flow |
| **4.5 Patching from Graph View** | Jumping directly to success block; Saving from graph view |
| **4.6 When to Use Graph Analysis** | Complex conditional logic; Switch statements; Nested if-else |

* **Lab Exercise:** Load GraphCrackMe.exe; use graph view to locate correct path without single-stepping; patch the binary.
* **Homework:** Solve GraphCrackMe2.exe using only graph view; submit patched binary.

#### Workshop 4.2: MA Track – Dynamic Analysis
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **4.1 Dynamic Analysis Goals** | What does the malware actually DO? No debugging required; Answer: files, registry, network, processes |
| **4.2 Process Monitor (ProcMon)** | Filtering by process name; File system activity; Registry activity; Process/Thread activity |
| **4.3 RegShot** | Taking "Before" snapshot; Executing malware; Taking "After" snapshot; Comparing changes; Exporting to text |
| **4.4 Wireshark Basics** | Capturing traffic; Display filters; Following TCP streams; Identifying C2 beacons |
| **4.5 TCPView / CurrPorts** | Viewing active connections; Which process connects where |
| **4.6 Combining Tools** | Workflow: RegShot Before → Execute → ProcMon capture → RegShot After → Wireshark capture → Revert VM |

* **Lab Exercise:** Take RegShot before/after; execute RAT_Demo.exe; analyze changes in ProcMon; capture network traffic in Wireshark.
* **Homework:** Analyze Dropper.exe – does it drop files? Which registry keys? Any network connections? Write 1-page behavioral report.

---

### Week 5: Code Caves & Memory Analysis

#### Workshop 5.1: RE Track – Code Caves & Code Injection
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **5.1 What Are Code Caves?** | Unused space in executable; Patterns of 00 or CC bytes; Why they exist (section alignment, compiler padding) |
| **5.2 Finding Code Caves** | Manual scanning in Memory View; Using x64dbg plugin (Find Code Cave); Calculating cave size |
| **5.3 Writing Shellcode in Debugger** | Assembly to byte conversion; Using the Assembler window; Testing shellcode before saving |
| **5.4 Redirecting Execution** | JMP instruction (E9); Short JMP (EB); CALL instruction; Modifying entry point |
| **5.5 Saving Modified Executables** | Patching cave contents; Redirecting original code; Maintaining functionality |
| **5.6 Use Cases** | Adding new features; Displaying messages; Bypassing checks; Code reuse |

* **Lab Exercise:** Inject code into HelloWorld.exe to print "Hacked!" before exiting; find code cave, write shellcode, redirect entry point.
* **Homework:** Inject code into Calculator.exe to display a message box on start; document the code cave address and JMP inserted.

#### Workshop 5.2: MA Track – Memory Analysis & Dumping
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **5.1 Why Dump Memory?** | Packed payload decrypts in RAM; Original unpacked code exists only in memory; You cannot analyze what you cannot see |
| **5.2 When to Dump** | After unpacking stub finishes; Before payload executes; Look for OEP (Original Entry Point) |
| **5.3 Memory Viewer in x64dbg** | Viewing memory regions; Memory protection flags (R, W, E); Searching for PE headers (MZ signature) |
| **5.4 Process Hacker Memory Dumping** | Right-click process → Memory; View memory regions; Dump to file; Suspending process before dump |
| **5.5 API Enumeration Count Trick** | API count increases dramatically after unpacking; Break when API count stabilizes; Indicator of OEP |
| **5.6 Dumping Workflow** | 1. Locate OEP; 2. Suspend process; 3. Dump memory region containing PE; 4. Save to disk; 5. Verify dumped file |

* **Lab Exercise:** Load packed malware; set breakpoint on `VirtualProtect`; step until OEP; dump memory region with MZ header; verify dumped file.
* **Homework:** Dump PackedSample2.exe independently; submit unpacked binary.

---

### Week 6: Advanced Debugging & Identifying Packers

#### Workshop 6.1: RE Track – Advanced Debugging Techniques
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **6.1 Conditional Breakpoints** | Break when condition is true; Syntax: `eax == 0x1234`; `[address] == byte/word/dword`; `strcmp` example |
| **6.2 Logging Breakpoints** | Break without pausing; Print values to log; Useful for tracing without interruption |
| **6.3 Memory Breakpoints** | Execute breakpoint (on code execution); Write breakpoint (on data modification); Read breakpoint (on data access) |
| **6.4 Hardware Breakpoints** | DR0-DR3 registers; Cannot be detected by simple anti-debug; Limited to 4 active |
| **6.5 Software Breakpoints** | INT3 instruction (0xCC); Modifies code; Easily detected; Unlimited number |
| **6.6 Trace Recording** | Recording every instruction executed; Finding where code came from; Performance impact |
| **6.7 Scripting in x64dbg** | x64dbg script language; Automating repetitive tasks; Conditional logic in scripts |

* **Lab Exercise:** Conditional breakpoint on `strcmp` to find correct serial; logging breakpoint on `VirtualAlloc` to log all allocations.
* **Homework:** Solve AdvancedCrackMe.exe using conditional breakpoints; submit serial key and explanation.

#### Workshop 6.2: MA Track – Identifying Standard & Custom Packers
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **6.1 Standard Packers** | UPX (open source); ASPack (commercial); MPRESS (Microsoft compiler); PECompact; Themida (advanced) |
| **6.2 UPX Unpacking** | `upx -d` command; Manual UPX unpacking (POPAD + JMP pattern) |
| **6.3 ASPack Characteristics** | Section names: `.aspack`, `.adata`; OEP pattern: POPAD, PUSH, RETN |
| **6.4 Custom Packers** | No packer signature; Unique section names (random strings); High entropy; Anti-debug tricks |
| **6.5 Indicators of Custom Packers** | Entry point not standard; Weird import table; Suspicious section permissions (RWX) |
| **6.6 Anti-Debug Techniques** | `IsDebuggerPresent`; `NtGlobalFlag`; Timing checks; INT3 detection; Software breakpoint detection |
| **6.7 Entropy as Detection Tool** | Calculating entropy; Packed files typically > 7.0; Unpacked files typically < 6.0 |

* **Lab Exercise:** Classify 4 samples: standard packers vs custom; unpack standard packers with tools; note suspicious indicators on custom.
* **Homework:** Classify 3 new samples: standard packer, custom packer, or not packed? Submit classification report.

---

### Week 7: Unpacking (Part 1) & Process Injection

#### Workshop 7.1: RE Track – Process Injection Techniques
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **7.1 Self-Injection** | Process allocates memory in itself; Executes new code in same process; Used by loaders and packers |
| **7.2 Remote Thread Injection** | Step 1: OpenProcess; Step 2: VirtualAllocEx; Step 3: WriteProcessMemory; Step 4: CreateRemoteThread |
| **7.3 Process Hollowing** | CreateProcess (suspended); NtUnmapViewOfSection (unmap original); VirtualAllocEx (allocate); SetThreadContext (redirect EIP); ResumeThread |
| **7.4 APC Injection** | QueueUserAPC; Asynchronous Procedure Calls; Thread must be in alertable state |
| **7.5 Reflective DLL Injection** | No call to LoadLibrary; DLL maps itself; Popular in Cobalt Strike |
| **7.6 Detecting Injection in Debugger** | Monitoring API calls; Examining memory regions; Looking for RWX permissions |

* **Lab Exercise:** Trace injector.exe; identify which injection technique is used; set breakpoints on key APIs; dump injected payload.
* **Homework:** Write 1-page report on the injection technique observed in provided sample.

#### Workshop 7.2: MA Track – Unpacking Packed Malware (Part 1)
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **7.1 Manual Unpacking Workflow** | 1. Load in debugger; 2. Find OEP; 3. Dump at OEP; 4. Fix IAT; 5. Rebuild executable |
| **7.2 Finding the OEP – POPAD/JMP** | Common for standard packers; POPAD restores registers; JMP to OEP |
| **7.3 Finding OEP – API Breakpoints** | Break on VirtualProtect/VirtualAlloc; Step until OEP; Watch for execution flow change |
| **7.4 Finding OEP – Memory Breakpoints** | Break on .text execution; Step until unpacking writes to .text |
| **7.5 Scylla Plugin Overview** | Dumping process; Finding IAT; Fixing imports; Rebuilding PE |
| **7.6 Dumping with Scylla** | Attach to process; Set OEP; Click Dump; Click Fix IAT; Rebuild with Dump + IAT |

* **Lab Exercise:** Unpack CustomPacked1.exe; find OEP using VirtualProtect breakpoint; dump with Scylla; fix IAT; verify unpacked binary runs.
* **Homework:** Unpack CustomPacked2.exe independently; submit unpacked binary and screenshot of fixed IAT.

---

### Week 8: Unpacking (Part 2) & Ghidra Analysis (Part 1)

#### Workshop 8.1: MA Track – Unpacking Packed Malware (Part 2)
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **8.1 Section Alignment Problems** | Raw Size vs Virtual Size mismatch; File on disk vs memory layout; Why dumped files crash |
| **8.2 Manual Section Alignment Fix** | Using PE-Bear; Changing Raw Address/Sizes; Matching virtual characteristics |
| **8.3 Unmapping Dumped Files** | Converting loaded memory back to disk format; Rebuilding section headers |
| **8.4 Re-Basing Executables** | Image Base mismatch; Relocation table (.reloc); Rebasing in PE-Bear |
| **8.5 Delphi Interactive Reconstructor** | Alternative unpacking tool; For Delphi-written malware; Reconstructing from memory |
| **8.6 Common Unpacking Pitfalls** | Dumping too early; IAT not fixed; Wrong OEP; Section alignment broken |

* **Lab Exercise:** Unpack BadAlignment.exe; dumped file crashes; fix section alignments manually; successfully run unpacked binary.
* **Homework:** Fix alignment on provided misaligned dump; submit working unpacked binary.

#### Workshop 8.2: RE Track – Analyzing Malware with Ghidra (Part 1)
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **8.1 Ghidra Overview** | NSA open source RE tool; CodeBrowser interface; Project management; Decompiler |
| **8.2 Ghidra vs IDA Pro vs x64dbg** | When to use each; Ghidra strengths (free, decompiler, scripting) |
| **8.3 Importing Binaries** | Creating new project; Import file; Selecting language (x86:LE:Windows) |
| **8.4 Auto-Analysis** | What analysis does; Finding entry point; Identifying functions; Creating cross-references |
| **8.5 CodeBrowser Interface** | Listing view; Decompiler view; Symbol tree; Data type manager; Console |
| **8.6 Navigation** | Going to address (G); Searching for strings; Following XREFs; Back/forward navigation |
| **8.7 Renaming Functions** | Changing `FUN_00401234` to meaningful names; Updating all references |

* **Lab Exercise:** Import unpacked malware into Ghidra; run auto-analysis; find `entry()`; rename 5 functions meaningfully; locate strings.
* **Homework:** Complete Ghidra worksheet (10 navigation tasks); submit Ghidra project file.

---

### Week 9: Advanced Ghidra & Post-Unpacking Analysis

#### Workshop 9.1: RE Track – Analyzing Malware with Ghidra (Part 2)
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **9.1 Finding C2 Servers** | Searching for strings (URLs, IPs, domains); Following XREFs to usage; Decoding obfuscated strings |
| **9.2 Identifying Encryption** | XOR loops (pattern: XOR [register], value); AES functions (substitution boxes); Custom encryption |
| **9.3 Extracting Encryption Keys** | Finding key in memory; Hardcoded keys; Derived keys |
| **9.4 Patching Analysis** | Modifying decompiled pseudocode; Patching instructions in Listing; Saving patched binary |
| **9.5 Creating Data Types** | Defining structures; Applying to buffers; Better decompilation |
| **9.6 Ghidra Scripting Basics** | Python in Ghidra; Automating analysis; Searching for patterns |

* **Lab Exercise:** Find hardcoded C2 in unpacked sample; identify XOR decryption loop; extract key; patch binary to connect to different C2.
* **Homework:** Write Ghidra analysis summary including C2 domain/port, encryption key, persistence mechanism.

#### Workshop 9.2: MA Track – Post-Unpacking Analysis
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **9.1 Full Static Analysis Workflow** | PE analysis → String extraction → Import analysis → Ghidra decompilation |
| **9.2 Extracting IOCs** | File hashes (MD5, SHA1, SHA256); IP addresses; Domains; Registry keys; Filenames; Mutexes |
| **9.3 YARA Basics** | Rule structure (rule name, meta, strings, condition); String types (text, hex, regex) |
| **9.4 YARA Conditions** | `any of them`; `all of them`; `$a and $b`; `#a > 3` (count); `@a == 0` (offset) |
| **9.5 Writing Effective YARA Rules** | Avoiding false positives; Using multiple string types; Metadata fields |
| **9.6 VirusTotal Submission** | Using API key; Private vs public submissions; Checking existing detections |
| **9.7 Malware Analysis Report Structure**| Executive summary; Static analysis; Dynamic analysis; Unpacking methodology; IOCs; YARA rule; Conclusion |

* **Lab Exercise:** Run unpacked payload through full static analysis; extract 5+ IOCs; write YARA rule; create detection signature.
* **Homework:** Finalize YARA rule for submission; prepare IOC list.

---

### Week 10: Capstone – Real-World Malware Analysis

#### Workshop 10.1: Capstone (Part 1) – Analysis & Unpacking
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **10.1 Capstone Scenario** | You received a suspicious file from an IR team; Determine if malicious; Extract all IOCs; Write report |
| **10.2 Capstone Sample Distribution** | Each student receives same sample (custom-packed RAT); No hints provided |
| **10.3 Independent Analysis (75 min)** | Static analysis; Packer identification; Dynamic analysis; Debugger tracing; OEP location; Memory dumping; IAT fixing; Ghidra analysis |
| **10.4 Instructor Check-in** | Progress review; Unblocking stuck students; Hint requests (limited) |
| **10.5 Report Drafting** | Template provided; Fill as you discover |

* **Lab Exercise (Independent):** Analyze capstone sample; produce draft report (sections 1-3).
* **Deliverable Due:** Draft capstone report (static analysis, dynamic analysis, unpacking progress).

#### Workshop 10.2: Capstone (Part 2) – Reporting & Graduation
* **Duration:** 2 hours

| Topic | Subtopics |
| :--- | :--- |
| **10.1 Report Finalization** | Complete all sections; Add IOCs; Attach YARA rule; Executive summary |
| **10.2 Student Presentations (5 min)** | Packer identified; Unpacking technique used; Malware capabilities; Key IOCs; Challenge faced |
| **10.3 Instructor Review** | Common mistakes; Best practices; Real-world applications |
| **10.4 Bootcamp Summary** | Top 5 unpacking techniques; Most useful API hooks; Recommended next steps |
| **10.5 Career Pathways** | Malware analyst; Reverse engineer; Incident responder; Threat intelligence |
| **10.6 Resources for Continued Learning**| Books; Blogs; Certifications (GREM, OSCP); Practice platforms |
| **10.7 Certificate Distribution** | PDF certificates; LinkedIn recommendation |

**Final Deliverable:** Complete malware analysis report including:
1. Static analysis findings
2. Dynamic behavioral analysis
3. Unpacking methodology (step-by-step)
4. Unpacked binary (submitted separately)
5. Ghidra analysis (C2, capabilities)
6. IOCs + YARA rule
7. Executive summary (1 paragraph for managers)

---