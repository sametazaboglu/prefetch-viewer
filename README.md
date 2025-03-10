# Windows Prefetch File Decompressor

Windows Prefetch File Decompressor is a tool designed to decompress Windows Prefetch files, which are utilized by the operating system to optimize application launch times. These files are compressed using the `RtlCompressBufferEx` function from the `ntdll.dll` library.

This script utilizes the `RtlDecompressBufferEx` function from the same library to decompress the Prefetch files. It takes two arguments: the input Prefetch file and the output file. The script reads the input Prefetch file, decompresses it, and writes the decompressed data to the output file.

In addition, the script performs a check on the file signature and the CRC checksum to ensure the integrity of the file. If the file signature or the CRC checksum is invalid, the script will terminate with an error message. Similarly, if the decompression process fails, the script will exit with an error message. If the size of the decompressed file does not match the original file size, the script will print a warning message.

## LEGAL DISCLAIMER 
This script is intended for research purposes only. The author is not responsible for any misuse or damage caused by this script. Use it at your own risk.

## Requirements
- Python 3.x
- Windows OS

## Installation

1. Clone the repository:
```bash
$ git clone https://github.com/sametazaboglu/prefetch-viewer.git
$ cd prefetch-viewer
```

2. Change the output folder location in the `main.py` script:

```python
# Output folder location
decompressed_prefetch_location = '<decompressed_folder_location>'
```

> [!NOTE]
> If you are changing the prefetch artifacts location, update the `compressed_prefetch_location` variable as well.

3. Run the script:
```bash
$ python main.py
```

## Usage
The script will automatically decompress all prefetch files located in `C:\\Windows\\Prefetch` and output them to the specified decompressed folder location.

## IO Class
The `IO` class provides common I/O operations. It includes methods to collect files with a specific extension from a directory (`collect_files`), decompress files in a directory (`decompress_files`), and read prefetch file data (`read_prefetch_file_data`).

## PrefetchDecompressor Class
The `PrefetchDecompressor` class is used to decompress the prefetch files. It uses the `RtlDecompressBufferEx` function from the `ntdll.dll` library to decompress the files.

## PrefetchData Class
The `PrefetchData` class is used to read the data from the decompressed prefetch files.

## COMPRESSED_FILE_HEADERS

The compressed Prefetch file starts with a `FILE_HEADER` structure, which contains information about the file. The structure is defined as follows:
```c
0x004d414d : DWORD Value; // 'MAM' ASCII | Compressed File Signature
0x53434341 : DWORD Value; // 'SCCA' ASCII | Decompressed File Signature
