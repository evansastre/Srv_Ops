# dd

```text
# dd [bs=<bytes>][cbs=<bytes>][conv=<keyword>][count=<block number>][ibs=<bytes>][if=<file >][obs=<bytes>][of=<file>][seek=<block number>][skip=<block number>][--help][--version]

# Dd can read data from standard input or file, convert data according to the specified format, and then output to file, device or standard output.

bs=<bytes> Set ibs (input) and obs (output) to the specified number of bytes.
Cbs=<bytes> When converting, only the specified number of bytes is converted at a time.
Conv=<keyword> Specifies how the file is converted.
Conv = ASCII Converts the EBCDIC code to an ASCIl code.
Conv = ebcdic Converts the ASCIl code to an EBCDIC code.
Conv = ibm Converts the ASCIl code to an alternate EBCDIC code.
Conv = block converts the change bits to fixed characters.
Conv = ublock converts a fixed bit into a variable bit.
Conv = ucase converts letters from lowercase to uppercase.
Conv = lcase converts letters from uppercase to lowercase.
Conv = notrunc does not truncate the output file.
Conv = swab exchanges each pair of input bytes.
Conv = noerror Does not stop processing when an error occurs.
Conv = sync adjusts the size of each input record to the size of ibs (filled with NUL).
Count=<block number> Reads only the specified number of blocks.
Ibs=<bytes> The number of bytes per read.
If=<file> Read from file.
Obs=<bytes> The number of bytes per output.
Of=<file> Output to file.
Seek=<block number> Skips the specified number of blocks at the beginning of output.
Skip=<block number> Skips the specified number of blocks at the beginning of reading.
--help help.
--version display version information
```

## Examples

```text
#1 whole disk data backup and recovery
#Backup:
dd if=/dev/hdx of=/dev/hdy
#Back up the local /dev/hdx disk to /dev/hdy

dd if=/dev/hdx of=/path/to/image
#Back up /dev/hdx full disk data to the image file of the specified path

dd if=/dev/hdx | gzip >/path/to/image.gz
#Back up /dev/hdx full disk data and compress it with gzip tool and save it to the specified path

#restore:
dd if=/path/to/image of=/dev/hdx
#Restore the backup file to the specified disk

gzip -dc /path/to/image.gz | dd of=/dev/hdx
#Restore the compressed backup file to the specified disk

#2. Use netcat remote backup
dd if=/dev/hda bs=16065b | netcat <targethost-IP> 1234
#Execute this command on the source host to back up /dev/hda

netcat -l -p 1234 | dd of=/dev/hdc bs=16065b
#Execute this command on the destination host to receive data and write to /dev/hdc

netcat -l -p 1234 | bzip2 > partition.img
                netcat -l -p 1234 | gzip> partition.img
#The above two instructions are the changes of the destination host command, 
respectively, using bzip2 gzip to compress the data, and save the backup file in the current directory.

#3. Backup MBR
#Backup:
dd if=/dev/hdx of=/path/to/image count=1 bs=512
#Back up the 512Byte size MBR information from the disk to the specified file.

#restore:
dd if=/path/to/image of=/dev/hdx
#Write the backed up MBR information to the beginning of the disk

#4. Backup floppy disk
dd if=/dev/fd0 of=disk.img count=1 bs=1440k
#Back up the floppy drive data to the disk.img file in the current directory

#5. Copy the memory data to the hard disk
dd if=/dev/mem of=/root/mem.bin bs=1024
#Copy the data in the memory to the mem.bin file in the root directory.

#6. Copy the iso image from the CD
dd if=/dev/cdrom of=/root/cd.iso
#Copy the disc data to the root folder and save it as a cd.iso file.

#7. Increase the Swap partition file size
dd if=/dev/zero of=/swapfile bs=1024 count=262144
#Create a file large enough (256M here)

mkswap /swapfile
#Turn this file into a swap file

swapon /swapfile
#Enable this swap file

/swapfile swap swap defaults 0 0
#Automatically load the swap file every time you turn it on, you need to add a line to the /etc/fstab file.

#8. Destroy disk data
dd if=/dev/urandom of=/dev/hda1
#Fill the hard drive with random data and use it to destroy data where necessary. 
#After doing this, /dev/hda1 will not mount, and the create and copy operations will not be performed.

#9. Get the most appropriate block size
#dd if=/dev/zero bs=1024 count=1000000 of=/root/1Gb.file
#dd if=/dev/zero bs=2048 count=500000 of=/root/1Gb.file
#dd if=/dev/zero bs=4096 count=250000 of=/root/1Gb.file
#dd if=/dev/zero bs=8192 count=125000 of=/root/1Gb.file
#By comparing the command execution time displayed in the dd command output, you can determine the optimal block size size of the system.
               
#10. Test hard disk read and write speed
dd if=/root/1Gb.file bs=64k | dd of=/dev/null
dd if=/dev/zero of=/root/1Gb.file bs=1024 count=1000000
#The read/write speed of the test hard disk can be calculated by the execution time of the last two commands.

#11. Repair the hard disk
dd if=/dev/sda of=/dev/sda
#When the hard disk is left unused for a long time (for example, 1, 2 years), 
#a magnetic flux point is generated on the disk. When the head reads these areas, 
#it encounters difficulties and may cause I/O errors. 
#When this situation affects the first sector of the hard disk, 
#it may cause the hard disk to be scrapped. 
#The above command has the potential to bring these data back to life. 
#And this process is safe and efficient.
```

