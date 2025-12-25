# Canon Smart Importer 📸

A PowerShell script that safely imports and organizes photos from your Canon DSLR camera's SD card to your computer.  This script intelligently handles timestamp corrections for FAT file systems and Daylight Saving Time adjustments, ensuring your photos maintain accurate metadata.

## ✨ Features

- **Safe Copy Operation**: Never modifies files on your SD card—only copies them
- **Automatic Organization**: Separates JPEGs and RAW (CR2) files into different folders
- **Timestamp Correction**: 
  - Handles FAT file system 2-second timestamp precision
  - Compensates for Daylight Saving Time differences
- **Smart Duplicate Detection**: Only copies new files, skipping duplicates
- **User-Friendly**: Interactive prompts guide you through the process
- **Preserves Directory Structure**: Maintains subfolder organization from your camera

## 🎯 Why Use This Script?

Canon DSLRs store photos on FAT32-formatted SD cards, which can cause timestamp discrepancies when copying to NTFS drives (Windows). Additionally, Daylight Saving Time changes can create 1-hour differences.  This script automatically corrects these issues using Robocopy's `/FFT` and `/DST` flags, ensuring your photo timestamps remain accurate.

## 📋 Prerequisites

- **Operating System**: Windows (PowerShell required)
- **PowerShell Version**: 5.1 or higher (built into Windows 10/11)
- **Permissions**: Ability to run PowerShell scripts (see Setup)

## 🚀 Quick Start

### 1. Download the Script

Clone this repository or download `Import-CanonPhotos.ps1`:

```bash
git clone https://github.com/YOUR-USERNAME/canon-smart-importer.git
cd canon-smart-importer
```

### 2. Enable PowerShell Scripts (First Time Only)

Open PowerShell as Administrator and run:

```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### 3. Run the Script

Right-click `Import-CanonPhotos. ps1` and select **"Run with PowerShell"**, or: 

```powershell
.\Import-CanonPhotos.ps1
```

### 4. Follow the Prompts

The script will ask for three paths: 

1. **Source Path**: Your SD card's photo folder (e.g., `E:\DCIM\100CANON`)
2. **JPEG Destination**:  Where to copy JPEG files (e.g., `C:\Photos\JPEGs`)
3. **CR2 Destination**: Where to copy RAW files (e.g., `C:\Photos\RAWs`)

**Example:**
```
STEP 1: Enter the FULL path to your source folder (e. g., E:\DCIM\100CANON)
E:\DCIM\100CANON

STEP 2: Enter the FULL path to your JPEG folder (e.g., C:\Users\mmkk2\Desktop\DSLR\Untouched\JPEGs)
C:\Photos\JPEGs

STEP 3: Enter the FULL path to your CR2 folder (e. g., C:\Users\mmkk2\Desktop\DSLR\Untouched\RAWs)
C:\Photos\RAWs
```

## 📂 Example Folder Structure

**Before (SD Card):**
```
E:\DCIM\
└── 100CANON\
    ├── IMG_0001.JPG
    ├── IMG_0001.CR2
    ├── IMG_0002.JPG
    └── IMG_0002.CR2
```

**After (Computer):**
```
C:\Photos\
├── JPEGs\
│   ├── IMG_0001.JPG
│   └── IMG_0002.JPG
└── RAWs\
    ├── IMG_0001.CR2
    └── IMG_0002.CR2
```

## 🔧 Technical Details

### Robocopy Flags Explained

| Flag | Purpose |
|------|---------|
| `/E` | Copies subdirectories, including empty ones |
| `/XX` | Excludes extra files present in destination but not source |
| `/FFT` | **FAT File Time** - Assumes 2-second granularity for timestamps |
| `/DST` | **Daylight Saving Time** - Compensates for 1-hour differences |
| `/NJH` | No Job Header (cleaner output) |
| `/NJS` | No Job Summary (cleaner output) |

### Why Robocopy? 

Robocopy (Robust File Copy) is built into Windows and specifically designed for reliable file copying with advanced timestamp handling—perfect for camera imports. 

## 🛡️ Safety Features

- **Read-Only Operation**: Your SD card files are never modified
- **Path Validation**: Checks that all folders exist before copying
- **No Overwrites**: Only copies new files (existing files are skipped)
- **Clear Feedback**: Shows progress and confirms completion

## ⚠️ Troubleshooting

### "Cannot be loaded because running scripts is disabled"

Run PowerShell as Administrator and execute:
```powershell
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
```

### "The source path does not exist"

- Ensure your SD card is inserted and recognized by Windows
- Use the exact path shown in File Explorer (e.g., `E:\DCIM\100CANON`)
- Don't add quotes around the path

### Files Not Copying

- Check that destination folders exist (create them first if needed)
- Ensure you have write permissions to destination folders
- Verify SD card is not write-protected (shouldn't matter for copying, but check anyway)

## 🤝 Contributing

Contributions are welcome! If you have suggestions for improvements: 

1. Fork this repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## 📝 To-Do / Future Enhancements

- [ ] Add support for other RAW formats (Nikon NEF, Sony ARW, etc.)
- [ ] Optional:  Organize files by date into subfolders
- [ ] Progress bar for large imports
- [ ] Config file for default paths
- [ ] Video file support (MOV, MP4)
- [ ] GUI version for non-technical users

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

- Inspired by the need for timestamp-accurate photo imports from Canon DSLRs
- Built with Windows Robocopy for maximum reliability
- Thanks to the photography community for feedback and testing

## 📬 Contact

**Your Name** - [@Cro-sby](https://github.com/Cro-sby)

Project Link: [https://github.com/Cro-sby/canon-smart-importer](https://github.com/Cro-sby/canon-smart-importer)

---

**⭐ If this script saved your photos' timestamps, please star this repo! **
