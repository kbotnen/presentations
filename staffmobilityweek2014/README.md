# BYOD Lockdown-exams roundup

### Fall 2013
## VDI vs In-House webbased solution
* VDI allows for examination in courses that needs extra software, i.e programming problems with syntax highlighing + compilers, latex editors, +++
* VDI allows heavily customization of the students experience, one desktop unique to each student (if we want / need too)
* Webbased solutions can be more lightweight and you dont need virtualisation infrastructure in serverroom
* Webbased solutions is less customizable on a pr.student basis
* Can use the In-House webbased solution through VDI

## SEB + VDI
* no support for third-party applications on Mac (we need to lockdown everything except the RDP Client)
* no integration with directoryservices (ActiveDirectory) so need some hacking / tweaking
* lockdown works as intended on Windows
* SafeExamBrowser is opensource and used by many facilities around Europe

## SEB + In-House webbased solution
* in-house webbased solution already developed and tested for other purposes
* integrated with authentication backend (Feide)
* integrated with our LMS (Mi-Side)
* lockdown works as intended on Windows and Mac

### Spring 2014
## Lanschool + VDI
* a solution primarly focusing on classroom management
* restrict applications, but not the explorer / finder process, thus allowing browsing of local files while in lockdown state
* supports all major platforms, osx, win, ios, linux, android +++
* best reporting and logging tools of the tested products
* $$$

## Inspera (SEB + Cloudbased solution)
* we dont know if it integrates with authentication backend (yet)
* cloudbased tools for creating and managing exams
* cloudbased tools for sensoring exams
* UiB is doing a exam with Inspera the spring 2014
* $$$

## Wiseflow (FLOWLock + Cloudbased solution)
* another lockdown browser, FLOWLock, not opensource
* cloudbased tools for creating and managing exams
* cloudbased tools for sensoring exams
* the create, managing and sensor tools are less sophisticated than Inspera
* UiB is doing a exam with Wiseflow the spring 2014
* $$$

### The conclusion?
* lockdown is the major issue
* few lockdown browsers available
* works mostly on Windows, sometimes on Mac and in the future, Linux?
* three different exams will be held spring 2014, and we will use the experience we gain to set the course for next semester


