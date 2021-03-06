# What's My Name?
Say my name, say my [name](myname.pcap).

# Solution
I used [Wireshark](https://www.wireshark.org/) to open the [pcap](https://en.wikipedia.org/wiki/Pcap) file and I found the flag in the dns lookup.

```
$ cat dns_lookup.txt 
0000   0a 00 27 00 00 16 08 00 27 66 da 17 08 00 45 00   ..'.....'fÚ...E.
0010   01 2e 92 54 40 00 40 11 22 0d c0 a8 02 0c c0 a8   ...T@.@.".À¨..À¨
0020   02 01 00 35 f5 b9 01 1a 18 fb aa a0 85 a0 00 01   ...5õ¹...ûª . ..
0030   00 09 00 00 00 00 0c 74 68 69 73 69 73 6d 79 6e   .......thisismyn
0040   61 6d 65 03 63 6f 6d 00 00 ff 00 01 c0 0c 00 01   ame.com..ÿ..À...
0050   00 01 00 00 01 2c 00 04 c0 a8 02 0d c0 0c 00 05   .....,..À¨..À...
0060   00 01 00 00 01 2c 00 09 06 6d 79 6e 61 6d 65 c0   .....,...mynameÀ
0070   19 c0 0c 00 0f 00 01 00 00 01 2c 00 04 00 05 c0   .À........,....À
0080   3e c0 0c 00 0f 00 01 00 00 01 2c 00 08 00 0a 03   >À........,.....
0090   6d 78 32 c0 3e c0 0c 00 0f 00 01 00 00 01 2c 00   mx2À>À........,.
00a0   08 00 14 03 6d 78 33 c0 3e c0 0c 00 02 00 01 00   ....mx3À>À......
00b0   01 51 80 00 06 03 6e 73 31 c0 3e c0 0c 00 02 00   .Q....ns1À>À....
00c0   01 00 01 51 80 00 06 03 6e 73 32 c0 3e c0 0c 00   ...Q....ns2À>À..
00d0   10 00 01 00 00 01 2c 00 37 36 70 69 63 6f 43 54   ......,.76picoCT
00e0   46 7b 77 34 6c 74 33 72 5f 77 68 31 74 33 5f 64   F{w4lt3r_wh1t3_d
00f0   34 39 34 36 66 35 31 32 35 66 63 33 31 35 63 66   4946f5125fc315cf
0100   62 36 32 31 35 30 62 36 65 32 61 65 62 65 37 7d   b62150b6e2aebe7}
0110   c0 0c 00 06 00 01 00 01 51 80 00 20 03 6e 73 31   À.......Q.. .ns1
0120   c0 0c 03 64 6e 73 c0 0c 5b 41 6e 3e 00 00 0e 10   À..dnsÀ.[An>....
0130   00 00 2a 30 00 01 51 80 00 00 0e 10               ..*0..Q.....
```

## Flag
```
$ cat flag.txt 
picoCTF{w4lt3r_wh1t3_d4946f5125fc315cfb62150b6e2aebe7}
```

## Hints
If you visited a website at an IP address, how does it know the name of the domain?
