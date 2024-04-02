
> [!WARNING]
> Due to inclusion of YARA, its worth going over these topics from sessional 1


# Lecture 4: Static malware analysis - 1
- Initial analysis method that involves
	- Extraction of useful information
	- Classification via informed decisions
	- Base for subsequent analysis
- Basic Static Analysis (I.F.E.U.C2)
	- Identifying a file
		- Analyze extension, magic byte, PE type,
	- Fingerprinting
		- Calculating SHA1, SHA256 & MD5 hashes.
		- Filenames not part of this, only the content is used
	- Extracting strings, function + metadata
	- Unpacking
	- Classifying and Comparing

# Lecture 5: PE + COFF
- PE aka COFF (Common Object File format)
- PE files do not contain PIE
- PE contains
	- Specifices where the exe needs to be loaded in memory
	- Reference for linking DLLs
	- Import/Export tables
	- Thread-Local Storage + Resource management data
- Components
	- Header
		- Structure
			- MZDOS > DOS STUB > PE FileHeader > Optional > Section Tables > Section
		- Metadata
			- Date, time, versions
			- Points + Offsets(RVAs) into sections where code and data are located
	- Sections
		- Stores data, code resources, directories + debug info
		- Important sections to note
			- DATA
				- .bss: Uninitialized global/static data
				- .rdata: ReadOnly data i.e. constants
				- .data: Stack data
			- RESOURCE
				- .rsrc: Images, icons, thumbnails, payload etc
			- EXE
				- .text: code i.e machine instructions
			- EXPORT
				- .edata: Exported symbols/functions
			- IMPORT
				- .idata: Imported symbols/functions
			- DEBUG
				- .debug: Debugging information such as symbol tables, line numbers
			- RELOCATE
				- .reloc: Holds information on how to relocate the exe in memory to a different address from the time it was linked

# Lecture 6: String Analysis
- Obfuscation/Packing
	- Used to protect the inner workings of the malware from security researchers, malware analysts + RE
	- Make it difficult to analyze the binary
- String analysis
	- Process of extracting readable characters and words from the malware
	- Types of strings to look for (Only gives a hint to what the malware is capable of)
		- File names
		- URL
		- IP addresses
		- Commands i.e. attack commands
		- Registry keys
# Lecture 7: YARA

Why YARA and not AWKSCRIPT
- Yara is specifically tailored for string matching
- AWK is tailored for log processing

```yara
to run a yara file use the following

$ yara32 -r yaraRule.yara fileToTestRule.exe
```


- Using hexadecimal strings
	- Good for using Jumps, Wildcards and alternatives.
		- Simple strings can also use wildcards but that involves regex
	- Wildcards = Use a "?" for each 4bits to guess
	- Jumps = Use when length of string is unknown. use \[3-5\] where 3 is minLen and 5 is maxLen
- Anonymous strings
	- Just use a \$. No need to name. Can only use the 'of them' condition for this though
- Global Rule
	- Impose restrictions on all rules within the file
- Private Rule
	- Disable the rule
- Iterative
	- same syntax as python.
	- example
	- for all i in (1,2,3):
		- (@a\[i\] + 10 == @b\[i\] )
	- This code checks if the first 3 letters of A are spaced 10 bytes apart from the first 3 letters of B and if they match or not

---

Extras copied from mattnotmax on github

## Basic Rule

Basic rule layout with suggested various meta descriptors.

```
rule specifc_name       // e.g. APT_CN_Winnti_exploit or crimeware_ZZ_RAT
{
    meta:               // suggested
        author = 
        date_created = 
        date_last_modified = 
        description = 
        filetype = 
        hash = 
        hash = 
        source = 
        TLP = 
        license = 
        min_yara_version = 
    
    strings:
        $a1 = "string type 1-1" ascii wide fullword nocase
        $a2 = "string type 1-2" 
        $a3 = "string type 1-3"

        $b1 = "string type 2-1"
        $b2 = "string type 2-2"
        $b3 = "string type 2-3"

        $c1 = "string type 3-1"
        $c2 = "string type 3-2"
        $c3 = "string type 3-3"
    
    condition:
        any of $a* or (2 of $b*) or (1 of $c*)
}
```

## Strings

- text strings are case sensitive.
- case insensitive can be used with `nocase` option.
- `wide` modifier can be used for UTF-16 formatting BUT not true UTF-16 support.
- `ascii` modifier can be used for ASCII encoding (default).
- `xor`  can be used to search for strings with a single byte xor applied to them.
- you can combine all types. E.g. `ascii wide nocase xor`.
- can write `xor (0x01-0xff)` for a specific range of xor bytes rather than all 255.
- `fullword` modifier guarantees that the string will match only if it appears in the file delimited by non-alphanumeric characters.
- use `fullword` keyword when string is short.

## Hexadecimal Strings

 - Hexadecimal strings allow three special constructions that make them more flexible: wild-cards, jumps, and alternatives.

### Wildcards
Wild-cards are just placeholders that you can put into the string indicating that some bytes are unknown and they should match anything.

The placeholder character is the question mark (?).

```
rule WildcardExample
{
    strings:
       $hex_string = { E2 34 ?? C8 A? FB }

    condition:
       $hex_string
}
```

### Jumps

Jumps can be used when the length of the content can vary or is unknown.

```
rule JumpExample
{
        strings:
           $hex_string = { F4 23 [4-6] 62 B4 }

        condition:
           $hex_string
}
```

### Alternatives

Alternatives can give a hex option similar to a regular expression.

```
rule AlternativesExample1
{
    strings:
       $hex_string = { F4 23 ( 62 B4 | 56 ) 45 }

    condition:
       $hex_string
}
```

## Regular Expressions

- They are defined in the same way as text strings, but enclosed in forward slashes instead of double-quotes.
- E.g. `/([Cc]at|[Dd]og)/`.
- can also be used in conjunction with `nocase`, `ascii`, `wide`, or `fullword`.
- Regular expression evaluation is inherently slower than plain string matching and consumes a significant amount of memory.

## Counting strings

The number of occurrences of each string is represented by a variable whose name is the string identifier but with a # character in place of the $ character.

```
rule CountExample
{
    strings:
        $a = "dummy1"
        $b = "dummy2"

    condition:
        #a == 6 and #b > 10
}
```
This rule matches any file or process containing the string $a exactly six times, and more than ten occurrences of string $b.

## File Size
- Can use bytes or append `KB` or `MB` as required.
- E.g. `filesize > 10KB`
- Don't use filesize modifier when scanning memory images.

## Offsets

The `at` modifier can be used to denote a decimal offset value (or vitual address for a running file).

The `in` modifier allows a range to be specified.

```
rule InExample_AtExample
{
    strings:
        $a = "dummy1"
        $b = "dummy2"
        $c = "dummy3"

    condition:
        $a in (0..100) and ($b in (100..filesize) or $c at 150)
}
```

## Conditions

Conditions are nothing more than Boolean expressions as those that can be found in all programming languages, for example in an if statement. They can contain the typical Boolean operators `and`, `or`, and `not`, and relational operators `>=`, `<=`, `<`, `>`, `==` and `!=`. Also, the arithmetic operators (`+`, `-`, `*`, `\`, `%`) and bitwise operators (`&`, `|`, `<<`, `>>`, `~`, `^`) can be used on numerical expressions.

## Checking File Headers
- if possible for speed and accuracy check the file headers.
- don't check file headers for memory images.

Examples:

PE Header
`uint16(0) == 0x5A4D`

ELF Header
`uint32(0) == 0x464c457f`

## Comments

```
/*
    This is a multi-line comment ...
*/
```

```
rule example { // this is a single line comment
```

## PE Module

The PE module allows you to create more fine-grained rules for PE files by using attributes and features of the PE file format.

Preface fule with `import "pe"`

see [PE Module](https://yara.readthedocs.io/en/stable/modules/pe.html#pe-module)


## Math Module

The Math module allows you to calculate certain values from portions of your file and create signatures based on those results.

Useful examples:

`math.entropy(0, filesize) >= 7`

## Rule Tips

- Don't use rules solely based on Windows APIs, this is prone to FPs.
- don't try to match on run-time generated strings (for disk files).
- don't put all criteria a necessary. Eg. not `all of them` but `five of them`.


### What to match

- Mutex
- Rare User Agents
- Registry Keys
- Typos
- PDB Paths
- GUIDs
- Internal module names
- Encoded or encrypted configuration strings


Use clusters of groups (See example at start). Eg:
- unique artifacts found in malware
- Win APIs
- File properties and structure (sections, entropy, timestamp, filesize etc.)

Then use these clusters to create the `condition`:
- `any of $a* or 5 of $b* or 2 of $c*`

## Random Tips

- Run command line with -p option to increase performance on SSDs.
- `pe.imphash() == "blah"` where `blah` needs to be lower case hex.
- loops vs strings: strings is faster.

## Random Rules from Kaspersky Webinar

Chinese language sameples, signed but not signed by MS, mimic legit Microsoft files by re-using their PE metainfo

```
condition:
    uint16(0) == 0x5A4D
    and filesize < 1000000
    and pe.version_info["Company Name"] contains "Microsoft" 
    and pe.number_of_signatures > 0
    and not forall i in (0..pe.number_of_signatures - 1):
        (pe.signatures[i].issuer contains "Microsoft" or pe.sigantures[i].issuer contains "Verisign")
    and pe.language(0x04 // LANG_CHINESE)
```

malware for AMD64 but compiled date before 64bit OS first released/created.

```
condition:
    uint16(0) == 0x5A4D
    and (pe.machine == pe.MACHINE_AMD64 or pe.machine == pe.MACHINE_IA64)
    and pe.timestamp > 631155661 // 1990-01-01
    and pe.timestamp < 1072915200 // 2004-01-01
    and filesize > 2000000
```