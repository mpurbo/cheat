# Character Encoding

- Get default character encoding
```powershell
[System.Text.Encoding]::Default
```
- Current character encoding
  - Input encoding
  ```powershell
  [console]::InputEncoding
  ```
  - Output encoding (standard console output)
  ```powershell
  [console]::InputEncoding
  ```
  - Pipe output encoding (output being sent through the pipeline to native applications)
  ```powershell
  $OutputEncoding
  ```
  - List available code pages
  ```powershell
  [System.Text.Encoding]::GetEncodings() | ft -AutoSize
  ```
  
