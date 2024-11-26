
# Introduction
QR codes are more efficient with _alphanumeric_ mode. `PAC-ID`s, thus only use characters `0–9`, `A–Z` (upper-case only) and `$*+-./,:`. If only one character is not in this set, the QR code becomes ~30% larger. 
For certain texts - in particular a `Display Name` - it is desirable that an extended character set can be used. 

In order to keep the efficent encoding of the PAC-ID as a whole, this extension is encoding a string with arbitratry unicode characters in base36.



# Specification

Extension type: `T.T`

The text MUST first be encoded in UTF-8.
The resulting bytes convert to base 36. 
- Big endianness.
- The alphabet is 01234567890ABCDEFGHIJKLMNOPQRSTUVWXYZ

The general idea:
- first encode text as utf-8 (note this will use variable number of bytes per character)
- the result encode an base36





## Implementation Caviats
Notes on base 36:
The alphabet is 01234567890ABCDEFGHIJKLMNOPQRSTUVWXYZ
While this is often assumed by libraries it is ultimately an arbirtrary choice. Be careful when using libraries.

decoding in python:
```
num = int(s36, 36) # this t
num_bytes = (num.bit_length() + 7) // 8
_bytes = num.to_bytes(num_bytes, byteorder='big')
```

decoding 
Be careful, decoding of longer base36 can overflow memory.


in javascript:
parseInt(s, base) (oddly) returns a float, which beyond 2^53 loses precision. One has to parse character wise:
```
let result = BigInt(0);
const base = BigInt(36);

 for (const char of base36String) {
        const digitValue = BigInt(parseInt(char, 36)); // Get digit value
        result = result * base + digitValue; // Accumulate the result
    }
```



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
