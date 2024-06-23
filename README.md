### README for Ollama on AMD GPUs

This guide explains how to set up and run Ollama on Windows using an AMD RX 6600 GPU. A precompiled version is available for easier installation.

## Precompiled Version

A precompiled version of Ollama can be downloaded and installed from [here](https://github.com/avnigashi/ollama-gfx1032/releases/download/alpha/OllamaSetup.exe.7z).

## Summary of Steps to Compile from Source

1. **Install MinGW**:
   ```powershell
   choco install mingw --force
   ```

2. **Clone the Ollama Repository**:
   ```powershell
   git clone https://github.com/ollama/ollama.git C:\Users\username\ollama
   ```

3. **Edit GPU List**:
   - Edit `gen_windows.ps1` to add support for `gfx1032` (RX 6600).

4. **Set Environment Variables**:
   ```powershell
   $env:HIP_PATH = "C:\Program Files\AMD\ROCm\5.7\bin"
   $env:ROCM_PATH = "C:\Program Files\AMD\ROCm\5.7\bin"
   ```

5. **Build Ollama from Source**:
   ```powershell
   cd C:\Users\username\ollama
   $env:CGO_ENABLED = "1"
   .\scripts\build_windows.ps1
   ```

6. **Run the Installer**:
   ```powershell
   Start-Process -NoNewWindow -Wait -FilePath "C:\Users\username\ollama\dist\OllamaSetup.exe"
   ```

## Additional Instructions

### ROCm Library Files for "Unsupported" AMD GPUs

1. **Navigate to ROCm Directory**:
   - Go to `%ProgramFiles%\AMD\ROCm\5.7\bin\rocblas\`.

2. **Backup the Library Folder**:
   - Make a backup of the current library folder.

3. **Download Optimized ROCm Libraries**:
   - For `gfx1032` (6600), use `Optimised_ROCmLibs_gfx1032.7z`.
   - For `gfx1031` (6700), use `Optimised_ROCmLibs_gfx1031.7z`.

4. **Extract and Replace Libraries**:
   - Extract the downloaded files and place them in the library folder, overwriting existing files.

## References

- Main source code: [Ollama on GitHub](https://github.com/ollama/ollama)
- Additional resources from [ROCmLibs](https://github.com/brknsoul/ROCmLibs)

## Notes

- **Main Source Code**: The current version is based on Ollama3.
- **Testing and Old Versions**: For testing purposes, older versions of ROCmLibs can be accessed on Dropbox. These libraries were pulled from YellowRoseCx's ROCm fork of KoboldCPP.
- **Removing `rocblasrt`**: If needed, manually delete the `rocblasrt.dll` file from `%ProgramFiles%\AMD\ROCm\5.7\bin\`.

### Contact

For support and contributions, please refer to the [Ollama GitHub repository](https://github.com/ollama/ollama)  [ROCmLibs](https://github.com/brknsoul/ROCmLibs) 
