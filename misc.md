# Miscellaneous Tools
Temporary collection until there is enough content for a separate file.

## Strings
* Identify sequence of characters with a minimum length: `strings -n 8 <filename>`
* Identify Unicode strings. Must be used with "wide" modifier: `strings -el <filename>`

## Hexdump
* Canonical hex and ASCII display: `hexdump -C <filename>`

## Yara

### Yara generation
[Yargen](https://github.com/Neo23x0/yarGen) - YARA rule generator

### Yara rules
[Github YARA rule repo](https://github.com/Yara-Rules/rules)

### Alternative Tools
[Loki](https://github.com/Neo23x0/Loki) - use to scan disk for Indicators of Compromise
[ClamAV](https://www.clamav.net/) - opensource antivirus that can run YARA rules. ClamAV has unpacking capabilities.
[Volatility](https://github.com/volatilityfoundation/volatility) - scans memory for artifacts.
