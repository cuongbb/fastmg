**FastMG: a simple, fast, and accurate maximum likelihood procedure to estimate amino acid replacement rate matrices from large data sets**
======================================================

**INSTALLATION**
============
_Users can either use precompiled tools on Linux or Mac 64-bit platforms or build tools from the source code_

**1. The splitting tools:**
:- _Tree based splitting method (recommended tool)_:  
:: +Option 1 (use precompiled tool)+: Uncompress either {"TreeBasedSplit_linux.zip (for Linux) or TreeBasedSplit_mac (for Mac)."} 
:: +Option 2 (compile tool from the source code)+: Uncompress TreeBasedSplit_sourceCodes.zip; Go into {"TreeBasedSplit_sourceCodes"} folder; run ./build (gcc version 4.4 is recommended).

:- _Random splitting method_:  Install Perl; then use the **RandomSplit.pl** Perl script.

**2. The estimating tool:**
:Install Perl; uncompress {"either estimate_mac.zip (for Mac) or estimate_linux.zip (for Linux)"}; use _estimate.pl_ tool to estimate an amino acid replacement matrix from alignments.


:Note that precompiled XRATE and PhyML programs used in the _estimate.pl_ are provided, however, users can build XRATE and PhyML programs from the source code: 
:- +Build XRATE  from the DART package+: {"Uncompress dart_sourceCodes.zip; Go into the dart_sourceCodes folder; run ./configure; make xrate (gcc version 4.4 is recommended)."}

:- +Build PhyML from PhyML package+: {"Uncompress  phyml_sourceCodes.zip;  Go into the phyml_sourceCodes folder; run ./configure; make (gcc version 4.4 is recommended)."}


**HOW TO RUN**
==========
The FastMG procedure consists of two phases: first, the large original alignments are split into non-overlapping sub-alignments by one of the alignment splitting algorithms (**Step 1**); then the matrix is estimated by joint maximum likelihood analysis of the smaller sub-alignments instead of the large original alignments (**Step 2**). 

**Step 1: Split alignments**
- Create a folder to contain all sub-alignments, for example  _subAlignments_.
- Use either TreeBasedSplit or RandomSplit to split alignments
: To use TreeBasedSplit tool (recommended tool):
:: _./TreeBasedSplit -k maxNumberOfSeqs -i alignmentFileName -z subAlignmentFolder_
:: For example:
:: _./TreeBasedSplit -k 16 -i sampleAlignment.phylip -z subAlignments_


: To use RandomSplit tool:
::  _perl RandomSplit.pl -k maxNumberOfSeqs -i alignmentFileName -z subAlignmentFolder_
:: For example:
:: _perl RandomSplit.pl -k 16 -i sampleAlignment.phylip -z subAlignments_


_Note that_: Input alignments must be in **sequential** PHYLIP format.


**Step 2: Estimate an amino acid model using the _estimate_ tool**		
:- Create a folder to contain all sub alignments such as Alignments. 
:- Copy all sub alignments into the created alignment folder
:- Run estimate tool as follows:
:: _perl estimate.pl -a alignmentFolder -s JTT.paml -o outputMatrixFile_
::where
:: -a: The folder of all sub alignments
:: -s: The file of starting matrix  in PAML format (default: JTT matrix as in JTT.paml)
:: -o: The file of the output matrix

:: For example:
:: _perl estimate.pl  -a Alignments -s JTT.paml -o testOutputMatrix.paml_


Note that: The folder of all sub alignments must be in same place with the estimate.pl script.

**NOTES**
=====

- FastMG is a collection of application programs: XRATE, PhyML, etc.

- FastMG uses the Maximum Likelihood method. It is faster, and more accurate than other tools.

- The package was written in C, C++ and Perl script.

_Note that_: FastMG is released under the GNU General Public License version 3 (GPLv3).