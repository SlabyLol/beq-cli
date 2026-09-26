# Building Beq-Cli for Windows and Linux

## Requirements

- Python 3.10+
- `pip install pyinstaller`
- The same dependencies as `requirements.txt` (torch is large)

## Linux (on a Linux machine)

```bash
pip install -r requirements.txt pyinstaller
pyinstaller --onefile --name Beq-Cli \
  --hidden-import beq_cli \
  --hidden-import beq_cli.model \
  --hidden-import beq_cli.processor \
  --hidden-import beq_cli.vision \
  --collect-all tokenizers \
  --collect-all rich \
  run.py
```

Binary appears in `dist/Beq-Cli`.

## Windows (on a Windows machine)

Same commands in PowerShell or cmd.

```powershell
pip install -r requirements.txt pyinstaller
pyinstaller --onefile --name Beq-Cli `
  --hidden-import beq_cli `
  --hidden-import beq_cli.model `
  --hidden-import beq_cli.processor `
  --hidden-import beq_cli.vision `
  --collect-all tokenizers `
  --collect-all rich `
  run.py
```

Result: `dist\Beq-Cli.exe`

## Notes

- Torch makes the binary hundreds of MB. For smaller distribution, use the Python source + venv.
- Cross-compiling from Linux to Windows is not supported by PyInstaller; build on the target OS (or use CI with both runners).
- First run still downloads the model weights into `./weights/`.

## Alternative: pip installable

```bash
pip install .
# then
beq-cli
```
