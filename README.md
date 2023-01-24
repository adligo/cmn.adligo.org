# cmn.adligo.org
This is the initial Classification Markup Notation implementation along with it's IETF RFC.  This is a general purpose binary format for streaming or storage which will compete with YAML, XML, JSON, Google Protocol Buffers and many other markup languages and APIs.  Although it is a binary format, the octects for labels and reserved characters are all UTF8 (and restricting to the single byte ASCII 7 UTF8 characters is really suggested for speed).  This allows piping of this format into files that any UTF8 compatable text editor SHOULD be able to read / render in most cases.  In some cases the binary octets MAY not render in a UTF8 compatable text editor, so eventually specialized viewers and editors MAY become useful.

## Classified Types
  Classification Markeup Notation classifies octets (bytes) and requires a schema in order to do so.  The following table summarizes the types;
  |  Type                |                      Comments                        | 
  |----------------------|------------------------------------------------------|
  | binary               |   See the section on binary and meta classification  |
  | boolean              |   t = true, f = false                                |
  | boolean list         |   See the section on boolean list below              |
  | complex list         |   See the section on complex lists below             |
  | decimal ten64        |   A binary decimal see ten64.adligo.org              |
  | integer ten64        |   A binary integer see ten64.adligo.org              |
  | integer list ten64   |   A list of integers see ten64.adligo.org            |
  | list                 |   See the section on lists below                     |
  | table                |   See the section on tables below                    |
  | text                 |   See the section on text below                      |
  | text segment         |   See the section on text segments below             |
  | text list            |   See the section on text lists below                |
  | object               |   See the section on objects below                   |
