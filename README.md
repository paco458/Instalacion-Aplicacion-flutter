# Instalar Flutter en Arch Linux

Guía completa para instalar y configurar Flutter en Arch Linux usando Fish Shell, Android Studio y Chromium.

---

# Requisitos

* Arch Linux
* Acceso sudo
* Conexión a internet
* Fish Shell (opcional)

---

# 1. Actualizar el sistema

```bash
sudo pacman -Syu
```

---

# 2. Instalar Flutter

Instalar Flutter desde los repositorios oficiales:

```bash
sudo pacman -S flutter
```

Verificar instalación:

```bash
flutter --version
```

---

# 3. Instalar yay (AUR helper)

Verificar si ya existe:

```bash
yay --version
```

Si no está instalado:

```bash
sudo pacman -S --needed base-devel git

git clone https://aur.archlinux.org/yay.git
cd yay
makepkg -si
```

---

# 4. Instalar Android Studio

Instalar Android Studio desde AUR:

```bash
yay -S android-studio
```

Abrir Android Studio:

```bash
android-studio
```

---

# 5. Configurar Android SDK

En Android Studio:

```text
More Actions → SDK Manager
```

Instalar:

* Android SDK
* Android SDK Platform
* Android SDK Build-Tools
* Android SDK Platform-Tools
* Android SDK Command-line Tools (latest)
* Android Emulator

La ruta normalmente será:

```text
/home/USUARIO/Android/Sdk
```

Verificar:

```bash
ls ~/Android/Sdk
```

Debe mostrar carpetas como:

```text
build-tools
cmdline-tools
platform-tools
platforms
```

---

# 6. Configurar Flutter con Android SDK

```bash
flutter config --android-sdk ~/Android/Sdk
```

Verificar:

```bash
flutter doctor
```

---

# 7. Instalar Chromium para Flutter Web

Instalar Chromium:

```bash
sudo pacman -S chromium
```

---

# 8. Configurar Chromium en Fish Shell

Si usas Fish Shell:

```fish
set -Ux CHROME_EXECUTABLE /usr/bin/chromium
```

Verificar:

```fish
echo $CHROME_EXECUTABLE
```

Resultado esperado:

```text
/usr/bin/chromium
```

---

# 9. Instalar Java

Flutter Android requiere JDK:

```bash
sudo pacman -S jdk17-openjdk
```

Verificar:

```bash
java -version
```

---

# 10. Aceptar licencias Android

```bash
flutter doctor --android-licenses
```

Aceptar todo con:

```text
y
```

---

# 11. Verificación final

```bash
flutter doctor
```

Resultado esperado:

```text
[✓] Flutter
[✓] Android toolchain
[✓] Chrome
[✓] Linux toolchain
[✓] Connected device
```

---

# 12. Crear un proyecto de prueba

```bash
flutter create hola
cd hola
```

Ejecutar en Linux:

```bash
flutter run -d linux
```

Ejecutar en Chrome:

```bash
flutter run -d chrome
```

---

# Problemas comunes y soluciones

## Error: Android SDK no encontrado

```text
Unable to locate Android SDK
```

Solución:

```bash
flutter config --android-sdk ~/Android/Sdk
```

Verificar que exista:

```bash
ls ~/Android/Sdk
```

---

## Error: cmdline-tools component is missing

```text
cmdline-tools component is missing
```

Solución:

Instalar desde:

```text
Android Studio → SDK Manager → SDK Tools
```

Marcar:

```text
Android SDK Command-line Tools (latest)
```

---

## Error: Android sdkmanager not found

```text
Android sdkmanager not found
```

Solución:

Instalar:

```text
Android SDK Command-line Tools (latest)
```

Luego verificar:

```bash
ls ~/Android/Sdk/cmdline-tools
```

---

## Error: Cannot find Chrome executable

```text
Cannot find Chrome executable at google-chrome
```

Solución:

Instalar Chromium:

```bash
sudo pacman -S chromium
```

Fish Shell:

```fish
set -Ux CHROME_EXECUTABLE /usr/bin/chromium
```

---

## Error usando Fish Shell con .zshrc

```text
source ~/.zshrc
```

Error:

```text
Uso no soportado de '='
```

Motivo:

Fish Shell no usa sintaxis de Bash/Zsh.

Usar:

```fish
set -Ux VARIABLE valor
```

---

## Error: No such file or directory ~/Android/Sdk

```text
/home/usuario/Android/Sdk: No such file or directory
```

Motivo:

El SDK Android todavía no fue instalado.

Solución:

Abrir Android Studio e instalar Android SDK.

---

# Comandos útiles

Actualizar Flutter:

```bash
flutter upgrade
```

Ver dispositivos:

```bash
flutter devices
```

Limpiar proyecto:

```bash
flutter clean
```

Obtener dependencias:

```bash
flutter pub get
```

---
