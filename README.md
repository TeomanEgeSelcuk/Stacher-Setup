# Merging Video and Audio with Stacher and FFmpeg

This guide explains how to set up Stacher on Windows to download the highest quality video and audio from YouTube and automatically merge them into a single MP4 file using FFmpeg and a custom batch script.

## Prerequisites

- **Operating System**: Windows (The process is specific to Windows, but similar steps can be followed on Linux and macOS with slight modifications.)
- **Tools Required**:
  - [Stacher](https://stacher.io/) (a GUI front-end for `yt-dlp`)
  - [FFmpeg](https://ffmpeg.org/) (a tool to handle multimedia files)

## Step-by-Step Guide

### 1. Install Stacher

1. Visit the [Stacher website](https://stacher.io/) and download the installer for your operating system.
2. Follow the installation instructions provided on the website to set up Stacher on your system.

### 2. Install FFmpeg

1. Download FFmpeg from the [official website](https://ffmpeg.org/download.html).
2. Extract the downloaded file to a location on your system (e.g., `C:\ffmpeg\`).
3. Add FFmpeg to your system's PATH:
   - Right-click on 'This PC' or 'My Computer' and choose 'Properties'.
   - Click on 'Advanced system settings' and then 'Environment Variables'.
   - Under 'System variables', find the `Path` variable and click 'Edit'.
   - Add the path to the `bin` folder inside your FFmpeg directory (e.g., `C:\ffmpeg\bin`).
   - Click 'OK' to save the changes.

### 3. Configure Stacher for Best Quality Downloads

1. Open Stacher.
2. In the download options, select `BestVideo+BestAudio`.
   - This ensures that Stacher will download the highest quality video and audio separately.

### 4. Create the Batch Script `merge.bat`

1. Open a text editor (e.g., Notepad) and paste the following code:

   ```batch
   @echo off
   ffmpeg -i "%1" -i "%2" -c:v copy -c:a copy "%~dpn1.mp4"
   ```

2. Save the file as `merge.bat` in a directory of your choice (e.g., `C:\scripts\merge.bat`).

### 5. Set Up the Custom Post Processing Command in Stacher

1. Open Stacher and go to **Settings**.
2. Find the **Custom Post Processing Command** section.
3. Paste the following command:

   ```bash
   C:\scripts\merge.bat "{1}" "{2}"
   ```

   - Replace `C:\scripts\merge.bat` with the actual path to where you saved the `merge.bat` file.

### 6. Download and Merge Video and Audio

1. Paste the YouTube URL into Stacher and start the download.
2. Stacher will download the best video and audio files separately.
3. After downloading, the `merge.bat` script will automatically merge the video and audio into a single MP4 file.

### 7. Verify the Output

- Once the process completes, check the output directory (the same as your download directory) for the final MP4 file. It should have the same name as the original video and contain both the video and audio merged.

## Troubleshooting

- If the merging fails, ensure that the file paths in the batch script and Stacher are correct.
- Check that FFmpeg is properly installed and accessible via the command line.

## References

- [Stacher Official Website](https://stacher.io/)
- [FFmpeg Official Website](https://ffmpeg.org/)
- [yt-dlp Documentation](https://github.com/yt-dlp/yt-dlp)
