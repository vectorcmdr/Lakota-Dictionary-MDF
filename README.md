# Lakota Language Dictionary (SFM/MDF & FLEx)

### A [Lakota language](https://en.wikipedia.org/wiki/Lakota_language) dictionary in SFM/MDF & FLEx format for the [Lakota people](https://en.wikipedia.org/wiki/Lakota_people) of the [Sioux tribes](https://en.wikipedia.org/wiki/Sioux).
#### Thank you to [u/Even-Morons-Dream](https://www.reddit.com/user/Even-Morons-Dream/) for the opportunity to help by reclaiming the data for them. I am honoured to be able to lend my skills.

## Usage:
For usage of the data, see the files within the \Lexicon folder.
It contains the following files for use:
* An SFM/MDF dictionary file ([dict.sfm](Lexicon/dict.sfm))
* A FieldWorks Language Explorer (FLEx) project backup ([Lakota Test 2025-06-28 1209 Lakota.fwbackup](Lexicon/Lakota%20Test%202025-06-28%201209%20Lakota.fwbackup))
* A FLEx import map ([dict-import-settings.map](Lexicon/dict-import-settings.map))
* An XHTML dictionary listing page ([Lexicon.xhtml](Lexicon/Lexicon.xhtml))

> [!IMPORTANT]  
>The [`.fwbackup`](Lexicon/Lakota%20Test%202025-06-28%201209%20Lakota.fwbackup) file can be loaded as a backup restore and used, edited, added to and exported from within FLEx.
> 
>The [`.xhtml`](Lexicon/Lexicon.xhtml) file can be browsed, though it is rudimentary at best.
> 
>The [`.sfm`](Lexicon/dict.sfm) file itself can be imported into FLEx / Soapbox / Toolbox or any SFM/MDF compatible language tool for building a dictionary.

## Methodology of Data Extraction:
> [!NOTE] 
>The data was retrieved from was a Unity binary built for Android, packaged as an `.apk`.

Analysis steps were as follows:
1. Unpack `.apk`.
2. Decompile `.dex` and check code for Android side keys or other info.
3. Identify Unity files within `assets` folder.
4. Identify libraries within `UnityServicesProjectConfiguration.json`.
5. Identify libraries within `RuntimeInitializeOnLoads.json`.
6. Identify libraries within `ScriptingAssemblies.json` and identify use of SqlCipher4Unity3D (_SQLCipher_).
7. Identify binaries as _mono_ and not IL2CPP.
8. Identify an obfuscated database outside of asset packs via header check (0->16:32 SQLCipher print) and disassembly of monobehaviour scripts as likely encrypted with SQLCipher.
9. Database likely contains additional text records and audio files due to output of heuristic analysis. _No key found_.
10. Merge `sharedassets0.assets.split[n]` into complete `sharedassets0.assets` file.
11. Run custom header lookup scripts in hex editor for Unity disassembly/unpacking and identify asset chunks (shaders, images, fonts, text, etc.)
12. Dump each data section to file.
13. Identify two sections are _SFM/MDF_ databases/dictionaries and are a single dictionary split in reverse due to size.
14. Merge SFM/MDF data and trim header + start/end padding.
15. Dump to _ASCII_ string.
16. Confirm output with native speaker.
17. Confirm data meets [technical documentation](_refs) / SIL International specs.
18. Import into _FLEx_.
19. Export FLEx project backup and xhtml.

## Raw Files:
The root of the repo contains more 'raw' extracted files:
* Dumped SFM/MDF data block 1 ([raw_data_A_to_I.bin](raw_data_A_to_I.bin))
* Dumped SFM/MDF data block 2 ([raw_data_I_to_Z.bin](raw_data_I_to_Z.bin))
* Extracted ASCII dictionary merged from fragments ([dict.txt](dict.txt))
* ASCII dictionary fragments ([dict_A_to_I.txt](dict_A_to_I.txt) + [dict_I_to_Z.txt](dict_I_to_Z.txt))

## Future Possibilities:
If time permits, I would like to branch the build script, table/library code and frontend from [STL Bitz Box](https://github.com/vectorcmdr/STL-Bitz-Box) & [ACNH Pattern Dump Index](https://github.com/vectorcmdr/ACNH-Pattern-Dump-Index) to create a static webpage dictionary for the data with a row entry per word and searchable/filterable columns for each piece of information tied to that word (including audio support) that can be updated, managed and hosted by the community and will be completely open source.
