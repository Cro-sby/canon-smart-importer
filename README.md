# Canon Smart Importer

A PowerShell script that copies photos from your Canon DSLR's SD card and fixes timestamp issues caused by FAT32 file systems and daylight saving time. 

## What It Does

- Copies files from your SD card (never modifies the originals)
- Automatically separates JPEGs and CR2 (RAW) files into different folders
- Fixes timestamp discrepancies from FAT32 SD cards
- Only copies new files (skips duplicates)

## Why? 

Canon cameras use FAT32-formatted SD cards, which can mess up file timestamps when you copy them to your computer. This script uses Robocopy's `/FFT` and `/DST` flags to handle the 2-second precision issue and daylight saving time differences.

## Requirements

- Windows 10 or 11 (PowerShell is built-in)
- That's it

## How to Use

### First Time Setup

1. Download `Import-CanonPhotos. ps1` from this repo
2. Open PowerShell as Administrator and run: 
   ```powershell
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```

### Running the Script

Right-click `Import-CanonPhotos.ps1` → **"Run with PowerShell"**

Or from PowerShell:
```powershell
.\Import-CanonPhotos.ps1
```

You'll be asked for three paths: 
1. Source (SD card): `E:\DCIM\100CANON`
2. JPEG destination: `C:\Photos\JPEGs`
3. CR2 destination: `C:\Photos\RAWs`

## Example

**SD Card:**
```
E:\DCIM\100CANON\
├── IMG_0001.JPG
├── IMG_0001.CR2
├── IMG_0002.JPG
└── IMG_0002.CR2
```

**After running:**
```
C:\Photos\
├── JPEGs\
│   ├── IMG_0001.JPG
│   └── IMG_0002.JPG
└── RAWs\
    ├── IMG_0001.CR2
    └── IMG_0002.CR2
```

## Robocopy Flags

| Flag | What it does |
|------|--------------|
| `/E` | Copy subdirectories |
| `/XX` | Don't copy extra files |
| `/FFT` | Fix FAT32 2-second timestamp issue |
| `/DST` | Fix daylight saving time differences |
| `/NJH /NJS` | Cleaner output |

## Troubleshooting

**"Cannot be loaded because running scripts is disabled"**
- Run PowerShell as Administrator:  `Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser`

**"The source path does not exist"**
- Make sure your SD card is plugged in
- Double-check the path (no quotes needed)

**Files aren't copying**
- Make sure the destination folders exist
- Check you have permission to write to those folders

## Future Ideas

- Support for other camera brands (Nikon, Sony, etc.)
- Organize files by date
- Video file support
- Maybe a GUI version

## License

MIT License - do whatever you want with it, just don't blame me if something breaks. 

See [LICENSE](LICENSE) for details.
