This is a fork of Proxmark for me to try and start implementing ISO/IEC 18092/ NFC Type 3/ Felica 
(since they all use the same frame structure) 



Original repository: https://github.com/Proxmark/proxmark3

Introduced changes:

  * Added a new FPGA bitstream for 212k Manchester modulation/demodulation and frame detection (snooping or tag simulation only) 
    (I did try to fit it into HF module, but ran out of FPGA slices)
  * Fixed a rather aggravating bug in fpga_compress.c, which prevented it from compressing more than two files.
  * Added 2 new functions to utilize the new bitstream (in hfsnoop.c), and corresponding client functions: 
    HfSnoopLite - (called as hf slite <frames>) would liten to the NFCIP frames it can recognize and dump them and the timing between frames to BigBuf
    HfSimLite - (called as hf litesim <BDEF2>) would at the moment only respond to POLL commands of NFCIP with specified NDEF2 in ts0
     (the names are artefact of the fact that I only had Felica Lite-S to test with)
  * Assuming that writing tracelen through buffer overflow was a bug, changed optimizedSnoop to set it explicitly
  * Changed hf list raw function to print a bytedump without table (in python list format), and write the same string to raws.txt file
  * Fiddled with Makefiles to make the result compile
  * Added a simple PRNG for use in shuffling cards in standalone mode

Notes: 
This is a personal hobby project, though I feel it might be of use in the main library. 
As such, it might not be developed further, since polling command turned out to be enough for my purposes.
There are many things that can be added:
 * Reaction to other commands, such as NFC Tag3 Block Read
 * Support for 414 kbit FeLica tags - only 212 is supported currently
 * Support for auth and encryption commands
 * Reader simulation - currently only snooping and primitive tag emulation are supported
 


