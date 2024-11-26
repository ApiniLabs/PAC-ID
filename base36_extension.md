
# Introduction
QR codes are more efficiently encoded with _alphanumeric_ mode, which uses a limited character set. If only one character is outside this set, the QR code becomes ~30% larger. `PAC-ID`s, thus only use characters `0–9`, `A–Z` (upper-case only) and `$*+-./,:`.  

For certain texts - in particular a `Display Name` - it is desirable that an extended character set can be used. 
This extension allows to use arbitrary unicode characters, which are encoded in base36. Although the encoded string will take up more space the PAC-ID as a whole can still be encoded in the efficient _alphanumeric_ mode.



# Specification

## Extension type
`T.T` must be used for this extension's `type`.

Example: `PAC-ID` of a balance, with a base 36 extension.
```
HTTPS://PAC.METTORIUS.COM/-MD/240:BAL500/21:210263*EXAMPLEOFBASE36$T.T/E4BLEW6R5EVD7XMGHG11


## Encoding
- The text MUST first be encoded in UTF-8.
- The resulting bytes MUST be converted to base 36 with the alphabet `01234567890ABCDEFGHIJKLMNOPQRSTUVWXYZ`. 

# Examples
``` 
Balance with Display Name "B-500 Balance"
HTTPS://PAC.METTORIUS.COM/-MD/240:BAL500/21:210263*N$T.T/E4BLEW6R5EVD7XMGHG11

Balance with Display Name "B-500 Balance @☣️Lab"
HTTPS://PAC.METTORIUS.COM/-MD/240:BAL500/21:210263*N$T.T/F92WF8NEUDFJX47Q8FLVASJ438FIDH87ZO2G2
```



## Terminology Used

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119](https://www.ietf.org/rfc/rfc2119.txt) "Key words for use in RFCs to Indicate Requirement Levels".

## FAQ

See [here](faq.md).

## License

Shield: [![CC BY-SA 4.0][cc-by-sa-shield]][cc-by-sa]

This work is licensed under a
[Creative Commons Attribution-ShareAlike 4.0 International License][cc-by-sa].

[![CC BY-SA 4.0][cc-by-sa-image]][cc-by-sa]

[cc-by-sa]: http://creativecommons.org/licenses/by-sa/4.0/
[cc-by-sa-image]: https://licensebuttons.net/l/by-sa/4.0/88x31.png
[cc-by-sa-shield]: https://img.shields.io/badge/License-CC%20BY--SA%204.0-lightgrey.svg
