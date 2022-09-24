# MOSTEK 38P70 Computer Example Code
## Compiling Example Code
The assembly code using this directory uses **[BespokeASM](https://github.com/michaelkamprath/bespokeasm)** as an assembler. The MOSTEK 3870 ISA configuration file can be found here. The command to compile the `af8` assembly code files in this directory is:

```sh
bespokeasm compile -e 2047 -p -c /path/to/mostek-3870.yaml assembly-code.af8
```

Where:

* `-e 2047` : generates a binary image with he maximum address of 2047, thus 2K bytes for a M2716 EPROM.
* `-p` : emit a pretty-print listing of the compiled assembly code.
* `-c /path/to/mostek-3870.yaml` : The path to the MOSTEK 3870 ISA BespokeASM configuration file found in the `examples` directory of the [**BespokeASM** repository](https://github.com/michaelkamprath/bespokeasm).
* `assembly-code.af8` : The MOSTEK 3870 assembly code to compile.

## Programming a M2716 EPROM with a MiniPro

Programming a vintage M2716 EPROM require a VPP of 25V per the data sheer. The MiniPro TL866II+ can at most generate a 18V VPP. The older TL866CS can generate a 21V VPP, so closer. There are a [few](https://youtu.be/IpQ3w7sMOYo) [YouTube](https://youtu.be/jrlxXsmqr-c) [videos](https://youtu.be/VwxCpSt-3RQ) that show how to boost the programming voltage on these programmers. I tried this with no success, but I am sure that was my fault. However, through some experimentation, I found that lengthening the programming pulse length allowed me to successfully program the M2716 with the TL866CS device. The minipro command is:

```sh
minipro -p M2716@DIP24 -w rom-data.bin --pulse 5000
```