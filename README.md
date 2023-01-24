# cmn.adligo.org
This is the initial Classification Markup Notation implementation along with it's IETF RFC.  This is a general purpose binary format for streaming or storage which will compete with YAML, XML, JSON, Google Protocol Buffers and many other markup languages and APIs.  Although it is a binary format, the octects for labels and reserved characters are all UTF8 (and restricting to the single byte ASCII 7 UTF8 characters is really suggested for speed).  This allows piping of this format into files that any UTF8 compatable text editor SHOULD be able to read / render in most cases.  In some cases the binary octets MAY not render in a UTF8 compatable text editor, so eventually specialized viewers and editors MAY become useful.

## Classified Types
  Classification Markeup Notation classifies octets (bytes) and requires a schema in order to do so.  The following table summarizes the types;
  |  Type                |                      Comments                        | 
  |----------------------|------------------------------------------------------|
  | binary               |   See the section on binary and meta classification  |
  | boolean              |   t = true, f = false                                |
  | booleanList          |   See the section on boolean list below              |
  | complexList          |   See the section on complex lists below             |
  | decimal              |   A arabic decimal                                   |
  | decimalList          |   A list of arabic decimals                           |
  | integer              |   A arabic integer                                   |
  | integerList          |   A list of arabic integers                          |
  | list                 |   See the section on lists below                     |
  | table                |   See the section on tables below                    |
  | ten64Decimal         |   A binary decimal see ten64.adligo.org              |
  | ten64Integer         |   A binary integer see ten64.adligo.org              |
  | ten64IntegerList     |   A list of integers see ten64.adligo.org            |
  | text                 |   See the section on text below                      |
  | textSegment          |   See the section on text segments below             |
  | textSegmentList      |   See the section on text lists below                |
  | object               |   See the section on objects below                   |

## Schema Objects
   Before any #CMN (from here on abbreviation for Classification Markup Notation) can be written or read a schema MUST exist.  #CMN schemas are comprised of #CMN objects which are grouped into packages simmilar to Java.  The following example illustrates a simple class object;
   ```
    {<class>
      name=MyPersonClass;
      package=org.example.mypackage;
      fields={
        firstName={class=textSegment;max=75;}
        lastName={class=textSegment;max=100;}
      }
    }
   ```
   
   This schema could be used to write a file that looked like this;
   ```
   { firstName=John; lastName=Doe; }
   ```
   Or optionaly if metadata was required, to later identify the class depending on the context.  It could be written as;
   ```
   {<org.example.mypackage.MyPersonClass> firstName=John; lastName=Doe; }
   ```
   
   ## Classification Markup Notation Text Escapes
   The following table illustrates the #CMN escapes, extending XML escapes with the semicolon escape &semi; Generally escapes
   should only be used when necessary.
   
   |  Original character  |  Escaped character  |
   |----------------------|---------------------|
   | &	                  | &amp;amp;           |
   | >	                  | &amp;gt;            |
   | <	                  | &amp;lt;            |
   | ;                    | &amp;semi;          |
   | "                    |	&amp;quot;          |
   | '                    |	&amp;apos;          |


## Binary
  One of the basic things missing from XML and JSON is a simple method to include binary.  The following illustrates a #CMN class that stores a image in binary;
  
   ```
    {<class>
      name=MyImageClass;
      package=org.example.mypackage;
      fields={
        bytes={class=binary;max=750;}
        type={class=textSegment;max=4;}
      }
    }
   ```
   Although it is impossible to illustrate how the bytes actually look in this webpage, it would look like this with &lt;bytesGoHere/&gt; representing the bytes in the file or stream;
   ```
   {<org.example.mypackage.MyImageClass>
     bytes=<size=97;><bytesGoHere/>;
     type=png;
   }
   ```
   Note that the semi colon after &lt;bytesGoHere/&gt; is NOT necessary, as the number of bytes 97 in this case, is provided by the metadata included in the bytes value section.
   
