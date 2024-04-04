# [`PAC-ID`](README.md) FAQ

**Q: Why is a PAC-ID represented as an HTTPS URL?**

**A:** The biggest advantage is that PAC-IDs can directly be entered as address into a browser (or scanned via QR code for example) on almost any device. To be able to easily recognize a PAC-ID as such, it was decided to use the subdomain `PAC.` instead of using a custom scheme like "PAC://".

**Q: Why is the subdomain "PAC." used?**

**A:** First of all, it's easy recognizable as a PAC-ID with this prefix/subdomain. Also, the `issuer` of a PAC-ID usually corresponds to the same domain name as the product manufacturer who distributed a PAC-ID. As most manufacturers are running a "www" web site on their main domain, usually under control of the marketing department, it is much easier to release a PAC-ID resolver on a subdomain than on a specific path like "/pac-id". See also question above on "Why is a PAC-ID represented as a HTTPS URL?".

**Q: Why is a PAC-ID all UPPER CASE?**

**A:** In order to minimize the size of the QR code. When limiting the character set to `0–9`, `A–Z` (upper-case only), `space` `$` `%` `*` `+` `-` `.` `/` `:`, QR codes use a very efficient encoding that only consumes 5 1⁄2 bits/character.

**Q: Why not using the ["tag:" scheme](https://en.wikipedia.org/wiki/Tag_URI_scheme)?**

**A:** The `tag:` URI scheme would not allow to form valid URLs. This was considered a major disadvantage, see also question above on "Why is a PAC-ID represented as a HTTPS URL?".

**Q: Is the usage of PAC-IDs limited to life science / laboratories?**

**A:** Not by design. In principle PAC-IDs could be used everywhere where real world objects need to be unambiguously identified and referred to among otherwise unrelated systems.

**Q: Are there any royalties for using a PAC-ID / implementing this specification?**

**A:** No, PAC-IDs may be freely used. The specification itself is licenced as "Creative Commons Attribution Share Alike 4.0".

**Q: Why not having a visual element inside the QR code?**

**A:** Putting an icon or any other visual element in the center of a QR code the free storage space for content will be decreased. Since we want the QR codes as small as possible wo placed the visual element next to the QR code. Also, rendering QR codes with an icon inside to a small display or label with low resolution is not that easy.

**Q: I have a better idea, how can I contribute?**

**A:** Create a new issue suggesting your contribution here: [PAC-ID Issues](https://github.com/ApiniLabs/PAC-ID/issues). Search if such an issue already exists. If you like, make changes, commit them and create a pull request for your changes to be reviewed and eventually merged.

**Q: I like that a PAC-ID points to my own (proprietary or local) service instances, e.g. to access my own ELN, LIMS, inventory system, ... How to achieve that?**

**A:** This is provided as a separate Smart Building Block named [PAC-Resolver](https://github.com/ApiniLabs/PAC-ID-Resolver).
