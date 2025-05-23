
## Introduction
QR codes are more efficiently encoded with _alphanumeric_ mode, which uses a limited character set. If only one character is outside this set, the QR code becomes ~30% larger. `PAC-ID`s, thus only use characters `0–9`, `A–Z` (upper-case only) and `$*+-./,:`.  

For certain texts - in particular a `Display Name` - it is desirable that an extended character set can be used. 
This extension allows to use arbitrary unicode characters, which are encoded in base36. Although the encoded string will take up more space the PAC-ID as a whole can still be encoded in the efficient _alphanumeric_ mode.


## Specification
- The text MUST first be encoded in UTF-8.
- The resulting bytes MUST be converted to base 36 with the alphabet `01234567890ABCDEFGHIJKLMNOPQRSTUVWXYZ`. 


## Examples
`"B-500 Balance"` is encoded as `"E4BLEW6R5EVD7XMGHG11"`
`"B-500 Balance @☣️Lab"` is encoded as `"F92WF8NEUDFJX47Q8FLVASJ438FIDH87ZO2G2"`


