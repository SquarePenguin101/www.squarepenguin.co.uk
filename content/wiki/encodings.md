## It's time for brain pain: Encodings

You almost certainly don't need to know this.  Really, you don't.  Continue to use get_iplayer as normal.  You only need to take an interest in encodings if you're having some problem using non-ASCII characters in search arguments, which is something you should virtually never need to do.  If you stick to ASCII for search arguments and stick to the default file naming behaviour, you shouldn't need to worry about encodings.

> Just say no to non-ASCII characters in file names

In order to support non-ASCII characters, get_iplayer must convert search arguments to Perl's internal encoding so that they can be tested against the BBC metadata in its cache.  In order to do that conversion, get_iplayer needs to know how the arguments were encoded for input.  The same thing applies for search results.  get_iplayer must know the encoding expected in order to convert from Perl's internal encoding.

In virtually every case, get_iplayer should be able to automatically detect the necessary encodings at run time. If not, something likely went wrong with the installation of the LWP (libwww-perl) Perl module, one of get_iplayer's dependencies.  To find out what values get_iplayer has detected run:

    get_iplayer --verbose dontshowanymatches

At the top of the output you should see some lines that look like:

    INFO: encodinglocale = UTF-8
    INFO: encodinglocalefs = UTF-8
    INFO: encodingconsoleout = UTF-8
    INFO: encodingconsolein = UTF-8
    INFO: ${^UNICODE} = 0
    
In the unlikely event you ever need to adjust the encodings detected by get_iplayer, the values can be overridden with the associated command-line options:

|Option|Description|
|------|-----------|
|`--encoding-locale`|encoding of command-line values, including search arguments|
|`--encoding-locale-fs`|encoding of file names, typically same as `--encoding-locale`|
|`--encoding-console-out`|encoding for STDOUT and STDERR, including search results|
|`--encoding-console-in`|encoding for STDIN (not currently used)|

Encoding names must be known to Perl.  A list can be found [here](http://search.cpan.org/~jhi/perl-5.8.1/ext/Encode/lib/Encode/Supported.pod). The encoding options cannot be saved in preferences or presets.

Encoding of search results may not always be perfect.  Any characters that don't map from Perl's internal encoding to that of your console may appear as XML character escapes in the form `&#x2019;` or as a replacement character.

If encodings are not automatically detected and not specified on the command line, the fallback encodings used are:

|Option|Windows|Linux/Unix/OSX|
|------|-------|--------------|
|`--encoding-locale`|cp1252 (Windows code page 1252)|UTF-8|
|`--encoding-locale-fs`|cp1252 (Windows code page 1252)|UTF-8|
|`--encoding-console-out`|cp850 (OEM ANSI code page 850)|UTF-8|
|`--encoding-console-in`|cp850 (OEM ANSI code page 850)|UTF-8|

The Windows fallback values are appropriate to UK English installations of Windows, but should more or less work for Windows systems with Western/Central European and American locales.  Most Linux/Unix/OSX users will have a system locale using UTF-8 encoding, so the fallback values should work.

If you use Windows with a system locale outside Western/Central Europe or the Americas, or Linux/Unix with a system locale that uses an encoding other than UTF-8, don't allow non-ASCII characters in file names because those characters may not map to your locale's encoding.  

> Just say no to non-ASCII characters in file names

There are many possible permutations of locale/language/encoding.  get_iplayer is developed to work with iPlayer which is (mostly) a UK-only service that uses the English language.  Inasmuch as get_iplayer has any sort of support policy, there is no promise to support Windows system locales other than UK English (with default code page settings) or Linux/Unix/OSX locales other en_GB.UTF-8.

#### Extra Esoteric Encoding Goodness

get_iplayer respects PERL_UNICODE and perl -C values, which are shown in the output above as the value of `${^UNICODE}`.