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
                  avr/  Xassembler.txt
                  avr/  config.txt
                    +----------------- avr/m328def.txt
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
