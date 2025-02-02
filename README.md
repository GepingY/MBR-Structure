# MBR-Structure
*This is a note regarding the structure of the general MasterBootRecord*
MBR is always the first `512 bytes` of the drive, here is the table of the structure <br/>
<br/>
| Bytes  | SumBytes | Description                                                                         |
|--------|----------|-------------------------------------------------------------------------------------|
| 001-440 | 440B     | MBR starts with 880 digits of hex of boot code                                       |
| 441-446 | 6B       | Then is 12 digits hex of Disk Signature                                              |
| 447-510 | 64B      | Then 128 digits hex of MBR partition table, each partition table has 32Digits hex or 16B |
| 511-512 | 2B       | Last 2B are the MBR boot signature 0x55AA                                            |
<br/>
As we can see, the sum of Bytes are 440+6+64+2=512B <br/>
Here is a example of a whole MBR <br/>

```
FA B8 00 10 8E D0 BC 00 B0 B8 00 00 8E D8 8E C0 FB BE 00 7C BF 00 06 B9 00 02 F3 A4 EA 21 06 00 00
BE BE 07 38 04 75 0B 83 C6 10 81 FE FE 07 75 F3 EB 16 B4 02 B0 01 BB 00 7C B2 80 8A 74 01 8B 4C 02
CD 13 EA 00 7C 00 00 EB FE 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 69 D0 E8 30 00 00 00 20 21 00 83 FE C2 FF 00 08 00 00 00 60 F6 24
00 FE C2 FF 07 FE C2 FF 00 68 F6 24 00 68 45 52 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 55 AA 
```
### Part 1: Boot Code Sector
As I mentioned above, the boot code has `440B`, hence `880 digits in hex`; in this case, the boot code would be from the start until `69`. <b/> 

The boot codes are written in assembly language, so we are not gonna interpret what these codes do here. <b/> 

Only bootable drives should need the boot codes. An external hard drive, which has the only purpose of data storage, shouldn't need those boot codes. In fact, this drive is an external hard drive as well, and it has those useless boot codes. In some cases, when you create the MBR on a non-bootable drive, the boot codes will still come along for some reason. But they shouldn't be necessary. In fact, if you replace them with 0, the drive should work just fine as well. <b/>

```
FA B8 00 10 8E D0 BC 00 B0 B8 00 00 8E D8 8E C0 FB BE 00 7C BF 00 06 B9 00 02 F3 A4 EA 21 06 00 00
BE BE 07 38 04 75 0B 83 C6 10 81 FE FE 07 75 F3 EB 16 B4 02 B0 01 BB 00 7C B2 80 8A 74 01 8B 4C 02
CD 13 EA 00 7C 00 00 EB FE 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00
```
### Part 2: Disk Signature
The next part of the MBR is the `6B` of `Disk Signature ` which has `12 digits` in hex. <b/>

The signature is how you identify your drive, in this case the signature is `69 D0 E8 30 00 00` <b/>

### Part 3: Partition Table
This part is from 447 to 510 consists of `64B`, they are the description of 4 partitions, in MBR maxmium of 4 partition is supported, each partition in the `64B` will have `16B` of their own, or `32 Digits hex`. In this case our Partition Table are `00 20 21 00 83 FE C2 FF 00 08 00 00 00 60 F6 24
00 FE C2 FF 07 FE C2 FF 00 68 F6 24 00 68 45 52 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00 00 00 00 00 00 00 00 00 00 00 00 00 00 00` <b/>

If we split them up into 4 equal sized bytes, then we will have the description for the 4 individual partitions. So <b/>
Partition 1
```
0020210083fec2ff000800000060f624
```
Partition 2
```
00fec2ff07fec2ff0068f62400684552
```
Partition 3
```
00000000000000000000000000000000
```
Partition 4
```
00000000000000000000000000000000
```
| Bytes  | SumBytes | Description                                                                         |
|--------|----------|-------------------------------------------------------------------------------------|
| 1 | 1B     | It tells you if the partition is bootable or non-bootable. If its 80 then it's bootable, if it's 00 then it's not bootable|
| 2-4 | 3B       | CHS of the first absolute sector in partition       |
| 5-6 | 1B      |tells you the partition type, for example 07 can be NTFS,exFAT,NFX,etc..... [Complete Table for partition type with given partition ID](https://en.wikipedia.org/wiki/Partition_type) |
| 7-9 | 3B       | CHS of the last absolute sector in partition                                            |
| 10-13 | 4B       | Logical block addressing of first absolute sector in the partition in litle-edian                                            |
| 13-16 | 4B       | Number of sectors in the partition, in litle-edian as well                                          |

This is a table of what each of the bytes mean, And this is how you decode them <b/>

Taking `Partition 1` as a example <b/>

1. The first bytes(2 digit of hex) is `00` meaning that this is a non-bootable partition <b/>

2. The Next `3B` is the CHS of the first absolute sector in partition which is `202100`, so it start at `Cylinder: 20` `Head: 21` `Sector: 00` <b/>

3. The next bytes is the code for the partition type, for example 07 can be NTFS,exFAT,NFX,etc..... But it might vary due to different OS. In this case the code is `83` which is `Linux EXT FileSystem`, since I created this partition, so I knows that this is acually a `ext4` partition. There is a python text array for the partitionID and it's corresponding Partition Type below <b/>

4. The Next `3B` is the CHS of the last absolute sector in partition which is `fec2ff`, so it ends at `Cylinder: fe` `Head: c2` `Sector: ff` <b/>

5. Then there is `4B` indicating Logical block addressing of first absolute sector in the partition, note that the hex of this is always in litle-edian, do you need to reverse it first and then turn it into decimal in order to know the acuall sector number. In this case the hex is `00080000`, to reverse the little-endian hex value 00080000 and convert it back into decimal: <b/>
   - Reverse the byte order: `00080000` → `00000800`
   - Convert 00000800 from hexadecimal to decimal, 00000800 (hex) = 2048 (decimal)

   So now we knows that the partition 1 starts from sector 2048 <b/>

6. The last `4B` indicate number of sectors in the partition, still `8 digits hex`, in this case is `0060f624`, do the same steps above, then you will get the number of number of sectors which is `620128256` if you did it correctly. Note that time it with the size of sector(normally `512B`) then you will get the size of the partition, `620128256 * 512 = 3.175056671x10^11`. Therefore this partition has total size of `317.51 GB`, but MBR it self won't tell you the sector size. <b/>

### Part 4: MBR boot signature
In the Master Boot Record (MBR), the last two bytes are always `55AA`, which is the boot signature. This signature indicates that the MBR is valid and can be used by the system's BIOS to load the bootloader. I've never seen a MBR without the `0x55 0xAA` <b/>

## Play Around
It's highly recommented to go through this decode proccess your self for once on your drive. <br />

You can read the MBR from the drive using this python script, and try to decode it yourself. make sure you replace `\\.\PHYSICALDRIVE1` with your acuall disk path, For Windows, the path should be something like `\\.\PHYSICALDRIVE1`. To find the list of disk paths on Windows, run `wmic diskdrive list brief`; for Linux, the path should look like `/dev/sdX`, where X is a letter from a to b, such as `/dev/sda`. Find the list of disk paths on Linux by using `lsblk`. **DO NOT** use the path to a partition instead of the path to disk on linux, there shouldn't be a number behind the path, e.g. you should use something like `/dev/sda` instead of `/dev/sda1` <br />

```python
disk_path = r'\\.\PHYSICALDRIVE1'
with open(disk_path, 'rb') as disk:
    raw_data = disk.read(512)
print(raw_data)
```
If you want to replace the boot code sector with 0 and see what happens, use this script(replace the path as well):
```python
def write_bytes_to_disk(offset, data):
    disk_path = r"\\.\PHYSICALDRIVE1"

    try:
        # Open the disk in raw mode
        with open(disk_path, 'r+b') as disk:

            disk.seek(offset)

            disk.write(data)
            print(f"Successfully wrote {len(data)} bytes to {disk_path} at offset {offset}.")
    except :
        print("Error")

# Example usage
if __name__ == "__main__":
    # Path to the disk (be very careful with this!)
    # Offset in bytes (e.g., 0 for the start of the disk)
    offset = 0

    # Data to write (hexadecimal string)
    hex_data = "000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000000069d0e83000000020210083fec2ff000800000060f62400fec2ff07fec2ff0068f62400684552000000000000000000000000000000000000000000000000000000000000000055aa"

    # Convert hex string to bytes
    data = bytes.fromhex(hex_data)

    # Write the data
    write_bytes_to_disk(offset, data)
```
replace the hex data with your acuall hex data, this hex bytes are a example, you see that I basically replaced the boot code sector with 0 and leave the rest the same. <br />

At last after you finish your own decoding, you can check if you did it correctly by this [repository](https://github.com/GepingY/PyPS/), or directly with this [program](https://github.com/GepingY/PyPS/blob/main/Main.py) <br />

## Report
If you find anything wrong with this note, please contact me through `ygp3737@gmail.com`
