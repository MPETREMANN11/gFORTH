<p>Hello,</p>
<p>Welcome to this FlashForth version meta-compilation project.</p>
<p>To make a meta-compilation, you need:</p>
<p>- have / install gForth (for Windows or Linux)</p>
<p>- run gForth</p>
<p>- in gForth, type:</p>
<pre>   include meta_AVR328.txt</pre>
<p>The project is evolving regularly.</p>

<h2>METACOMPILATION</h2>
<p>To generate a version of the FORTH language, there are three solutions:</p>
<ul>
   <li>build the code in assembly language</li>
   <li>uses code in C language</li>
   <li>use the FORTH language and go through a meta-compiler.</li>
</ul>
<p>The project presented here uses a metacompiler written in FORTH language.</p>

<h3>The PHENIX meta-compiler</h3>
<p>To generate a version of the FORTH language, there are three solutions:</p>
<ul>
   <li>build the code in assembly language</li>
   <li>uses code in C language</li>
   <li>use the FORTH language and go through a meta-compiler.</li>
</ul>
<p>The project presented here uses a metacompiler written in FORTH language</p>
<p>The PHENIX meta-compiler was built in 1988 and used successfully on a 16-bit FORTH version under MS-DOS.</p>
<p>I am in the process of adapting it to gForth in order to generate executable code for any target.</p>
<p>For the moment, the project favors the processor of ARDUINO cards.</p>
<p>Here is the sequence diagram of the files allowing the generation of code for ARDUINO: </p>
<pre>
meta_AVR328.txt
  +-------------- forthExtend.txt
                  meta.txt
                    +----------------- compile-header-resolve.txt
                                         +-------------------- avr/  FFmetaHeader.txt
                  avr/  Xassembler.txt
                  avr/  config.txt
                    +----------------- avr/  m328def.txt
                  avr/  macros.txt
                  avr/  core.txt
                  kernelCode.txt
</pre>
<h3>Project files</h3>
<h4>meta_AVR328.txt</h4>
<p>Contains a succession of calls to the files necessary to compile a target compatible with ARDUINO NANO or UNO cards.</p>

<h4>forthExtend.txt</h4>
<p>Contains a few words to make part of the meta.txt code compatible with gForth.</p>

<h4>meta.txt</h4>
<p>Contains the PHENIX meta-compiler being adapted to gForth and debugged to generate code for a target.</p>

<h4>avr/  Xassembler.txt</h4>
<p>Contains the AVR assembler written in FORTH and compatible with gForth. This assembler can only generate AVR code, therefore not executable by gForth.</p>

<h4>avr/  config.txt</h4>
<p>Contains configuration data for an AVR target.</p>

<h4>avr/m328def.txt</h4>
<p>Fichier appelé par config.txt</p>
<p>Contient des données de configuration pour une cible AVR328.</p>

<h4>avr/  macros.txt</h4>
<p>Contains macro instructions that complement Xassembler.</p>

<h4>avr/  core.txt</h4>
<p>Contains the part of the FORTH kernel written in AVR assembler.</p>

<h4>kernelCode.txt</h4>
<p>Contains the part of the FORTH kernel written in FORTH.</p>

<h3>Meta-compilation vocabularies</h3>
<p>Meta-compilation vocabularies All the difficulty in understanding a metacompiler lies
in the ambiguity of words. It is not possible to escape this ambiguity insofar as the system created uses the language of
creative system. We are talking here about host-system and target-system. The ambiguity is further increased by the fact that a good metacompiler is
"homologous": it compiles "like" a usual compiler, that is to say that the target is written in natural Forth as if the code
had to be a simple extension of the host. Gold target, system complete and autonomous, cannot of course be a subset of
the host: it must reside outside it.</p>
<p>To remove the ambiguity of words, FORTH uses its concept of VOCABULARIES. The same word will have a different meaning depending on
that it belongs to this or that vocabulary. This is the CONTEXT, that is say the list of vocabularies active at a given time, which allows
to the host system to know what is the meaning of all homonyms word to interpret. The management of vocabularies in metacompilation is
a key step which conditions the whole process.</p>

<h4>ROOT</h4>
<p>ROOT is the minimal vocabulary of the language. It serves essential to manage the use of other vocabularies in the context
using the ONLY ALSO concept.</p>

<h4>FORTH</h4>
<p>FORTH is the usual host vocabulary. It is used to define all memory access, interpretation,
compilation, metacompilation. Most of his words will get- sure of the homonyms in the target since it is the aim of the
metacompilation.</p>

<h4>XASSEMBLER</h4>
<p>XASSEMBLER is the cross assembler.</p>

<h4>META</h4>
<p>META is the master vocabulary of metacompilation. It's him which contains all the metacompiler interpretation words. He
is further enriched during the metacompilation of a number references of the target in the form of labels, constants,
of variable addresses that it may need later.</p>

<h4>TARGET</h4>
<p>TARGET is the target vocabulary. We must understand that TARGET is not the chaining of words as they are compiled
in the target: it is a vocabulary of the host which only keeps the addresses of these words in the target. It is therefore rather the image of
the target or if you want a table of references for the target. All the TARGET words have the same structure: at runtime, they compile
in the target the executive code of a word of the target already metacompiled.</p>

<h4>FORWARD</h4>
<p>FORWARD is the vocabulary of references before. It's a vocabulary in all points comparable to TARGET but whose words
correspond to references not yet defined in the target. AT execution these words form a chain of addresses where must be compile a reference 
until the time this reference is set which makes it possible to "resolve" this chain of addresses left in suspense. It is obvious that the 
metacompilation must end with a FORWARD vocabulary fully resolved on pain of leaving
"blanks" in the target code.</p>

<h4>TRANSITION</h4>
<p>TRANSITION is the structural vocabulary. It is him who contains the words of immediate interpretation of the structures of
control as IF ELSE THEN when the metacompiler is itself in high-level compilation state in the target. It is META which
decides to activate TRANSITION when it metacompiles definitions in target.</p>

<h4>USER</h4>
<p>USER is the metacompilation vocabulary of USER type words. Just as FORTH's USER vocabulary contains homonyms
of FORTH to define user words (mainly for the multitasking), this second USER vocabulary contains homonyms of
META to define the same type of words in the target.</p>
<hr/>

<p>It is important that the metacompiler has words allowing establish the context vocabularies at all times as well as
the current vocabulary where new words are added. It is not not useless even to provide synonyms in META insofar as
this will quickly load with references with names vocabularies of the target. So the word FORTH in META no longer fits
place FORTH in CONTEXT but reference the FORTH vocabulary from the target: use the immediate synonym [FORTH] to talk about
FORTH vocabulary of the host.</p>

<p>META words like IN-META, IN-TRANSITION, IN-TARGET, defined at the start of the metacompiler are fundamental: it is their forgetfulness or misuse
who are responsible for so many errors or misunderstandings of metacompilation.</p>

<h2>The TARGET</h2>
<p>The target system is always inert to the host system. For this one, it is only about a series of addresses where is compiled a
code that is foreign to it. At the end of metacompilation, this zone will be saved and the user can exit the host system to launch
the new system.</p>
<p>Regardless of the metacompilation site chosen, the metacompiler must first have a series of words very
simple to read or write on this site as well as a pointer advancing through metacompilation in this space. Through
analogy with the basic compiler words forth <b>@ C@ ! C! DP HERE ALLOT , C,</b> the metacompiler has the words <b>@-T C@-T !-T C!-T
   DP-T HERE-T ALLOT-T ,-T C,-T</b> etc which are sufficient for him to define by the following all operations on the target. This portion of the
   metacompiler is specific: its change allows to consider any other internal or external metacompilation site.</p>
<p>These same memory access words to the temporary construction site of the target will also be used to force the assembler to
  Assemble code only in this placeholder.</p>




