# Aurora Music — descargas

Reproductor de música local para **Windows**, **Linux** y **macOS**. Reproducción sin pausas entre pistas,
ecualizador de 10 bandas, visualizador, biblioteca con búsqueda instantánea, favoritos y listas. Interfaz en español.

Este repositorio solo contiene los **instaladores**. Descárgalos desde **[Releases](../../releases/latest)**. El
código fuente está en [Erik7746/Aurora-Music](https://github.com/Erik7746/Aurora-Music).

Ningún paquete necesita Java: todos llevan su propio runtime. Aurora lee tu música, pero **nunca modifica, mueve ni
borra tus archivos**.

---

## ¿Qué archivo descargo?

| Sistema | Archivo | Recomendado para |
|---|---|---|
| Windows 11 x64 | `Aurora Music-1.2.0.msi` | La mayoría de usuarios de Windows |
| Windows 11 x64 | `Aurora Music-1.2.0.exe` | Instalador alternativo, si prefieres un `.exe` |
| Debian, Ubuntu, Linux Mint, Pop!_OS | `aurora-music_1.2.0_amd64.deb` | Distribuciones basadas en Debian |
| Arch Linux, Manjaro, EndeavourOS | `aurora-music-1.2.0-1-x86_64.pkg.tar.zst` | Distribuciones basadas en Arch |
| Cualquier Linux x64 | `Aurora_Music-1.2.0-x86_64.AppImage` | Sin instalar nada, o si tu distribución no aparece arriba |
| macOS 11 o superior | `Aurora Music-1.2.0.dmg` | Mac |

> Sustituye `1.2.0` por la versión que descargues.

---

## Windows

### MSI (recomendado)

1. Haz doble clic en `Aurora Music-1.2.0.msi`.
2. Si aparece SmartScreen («Windows protegió su PC»), pulsa **Más información** → **Ejecutar de todas formas**. El
   instalador no está firmado con un certificado de pago, por eso aparece el aviso.
3. Sigue el asistente. Se instala **solo para tu usuario**, sin permisos de administrador, en
   `%LOCALAPPDATA%\Programs\Aurora Music`, con accesos en el menú Inicio y en el escritorio.

Instalación sin asistente, desde PowerShell, en la carpeta de la descarga:

```powershell
msiexec /i "Aurora Music-1.2.0.msi" /qn
```

### EXE

Haz doble clic en `Aurora Music-1.2.0.exe` y sigue el asistente. Si SmartScreen lo bloquea, aplica el mismo paso que
con el MSI. Instala Aurora en el mismo sitio, así que basta con usar uno de los dos.

### Actualizar y desinstalar

- **Actualizar**: instala la versión nueva encima. Tu biblioteca y tus ajustes se conservan.
- **Desinstalar**: Configuración → Aplicaciones → Aplicaciones instaladas → *Aurora Music* → **Desinstalar**.

---

## Linux

Aurora necesita ALSA y GTK 3, que cualquier escritorio actual ya tiene. El sonido sale por PipeWire o PulseAudio.

### Debian, Ubuntu y derivadas (`.deb`)

```bash
sudo apt install ./aurora-music_1.2.0_amd64.deb
```

Desinstalar:

```bash
sudo apt remove aurora-music
```

### Arch Linux y derivadas (`.pkg.tar.zst`)

```bash
sudo pacman -U aurora-music-1.2.0-1-x86_64.pkg.tar.zst
```

Desinstalar:

```bash
sudo pacman -R aurora-music
```

Con los dos paquetes, Aurora se instala en `/opt/aurora-music` y aparece en el menú de aplicaciones (*Sonido y
vídeo*). El paquete de Arch añade además el comando `aurora-music` para abrirlo desde la terminal.

### AppImage (cualquier distribución)

No se instala: es un único archivo que se ejecuta directamente.

```bash
chmod +x Aurora_Music-1.2.0-x86_64.AppImage
```

```bash
./Aurora_Music-1.2.0-x86_64.AppImage
```

Si no arranca por un error de FUSE (`libfuse.so.2` no encontrado), instala FUSE 2 (`sudo apt install libfuse2t64` en
Ubuntu 24.04, `libfuse2` en versiones anteriores, `sudo pacman -S fuse2` en Arch), o ejecútalo sin FUSE:

```bash
./Aurora_Music-1.2.0-x86_64.AppImage --appimage-extract-and-run
```

Para desinstalarlo, borra el archivo.

---

## macOS

1. Abre `Aurora Music-1.2.0.dmg` y arrastra **Aurora Music** a la carpeta **Aplicaciones**.
2. La primera vez, macOS la bloquea porque la app no está notarizada por Apple. Para abrirla:
   - En el Finder, **clic derecho** sobre Aurora Music → **Abrir** → **Abrir**.
   - En macOS 15 o superior: intenta abrirla una vez y luego ve a **Ajustes del Sistema** → **Privacidad y
     seguridad** → **Abrir igualmente**.

   O desde la Terminal:

```bash
xattr -dr com.apple.quarantine "/Applications/Aurora Music.app"
```

Si al abrirla la app se cierra sola en una máquina virtual sin aceleración gráfica (Metal), ábrela con el dibujo por
software:

```bash
AURORA_PRISM_ORDER=sw "/Applications/Aurora Music.app/Contents/MacOS/Aurora Music"
```

**Desinstalar**: arrastra *Aurora Music* desde Aplicaciones a la Papelera.

> El `.dmg` está compilado para Mac con Intel. En un Mac con Apple Silicon (M1 o posterior) se ejecuta con Rosetta 2,
> que macOS ofrece instalar la primera vez. Apple Silicon todavía no se ha probado.

---

## Primeros pasos

1. Abre Aurora Music.
2. Ve a **Carpetas locales** → **Añadir carpeta** y elige la carpeta donde guardas tu música.
3. Aurora lee las canciones y las organiza por álbum y artista. A partir de ahí detecta sola la música nueva.

Formatos: MP3, FLAC, Ogg Vorbis, Opus, WAV y AIFF en todos los sistemas; AAC/M4A en Windows y macOS.

---

## Tus datos

Desinstalar o actualizar **no borra** tu biblioteca, tus favoritos, tus listas ni tus ajustes. Si quieres borrarlos
también, elimina estas carpetas a mano:

| Sistema | Carpetas |
|---|---|
| Windows | `%LOCALAPPDATA%\Aurora Music` |
| Linux | `~/.local/share/aurora-music`, `~/.cache/aurora-music`, `~/.local/state/aurora-music` |
| macOS | `~/Library/Application Support/Aurora Music`, `~/Library/Caches/Aurora Music`, `~/Library/Logs/Aurora Music` |

Tu música nunca se toca.

---

## Comprobar la descarga (opcional)

Compara el resultado con la suma SHA-256 publicada en la página del release.

Windows (PowerShell):

```powershell
Get-FileHash "Aurora Music-1.2.0.msi" -Algorithm SHA256
```

Linux:

```bash
sha256sum aurora-music_1.2.0_amd64.deb
```

macOS:

```bash
shasum -a 256 "Aurora Music-1.2.0.dmg"
```

---

## Problemas frecuentes

| Problema | Solución |
|---|---|
| Windows: SmartScreen no deja instalar | **Más información** → **Ejecutar de todas formas** |
| macOS: «no se puede abrir porque Apple no puede comprobarla» | Clic derecho → **Abrir**, o el comando `xattr` de arriba |
| Linux: el AppImage no arranca | Instala FUSE 2 o usa `--appimage-extract-and-run` |
| «Audio no disponible» al abrir | Reinstala Aurora. En Ajustes → Diagnóstico → *Motor de audio* se ve qué archivo falla |
| No aparecen canciones nuevas | **Carpetas locales** → **Actualizar** |

Los registros para informar de un problema se abren desde **Ajustes → Diagnóstico → Registros**.

---

## Licencia

Aurora Music usa la biblioteca de audio **BASS** (un4seen), que es gratuita solo para **uso no comercial**. Los avisos y
licencias de todos los componentes de terceros van incluidos en la instalación.
