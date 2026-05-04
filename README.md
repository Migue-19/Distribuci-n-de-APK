# Distribución de APK con Firebase App Distribution

**Repositorio:** [URL de tu repositorio aquí]  
**Autor:** Miguel Angel Ruiz Urmendis  
**Correo:** miguelangelruizurmendis@gmail.com  
**Versión actual:** 1.0.1+2  
**Fecha:** Mayo 2026

---

## 📋 Descripción

App Flutter conectada a Firebase, distribuida mediante **Firebase App Distribution** para pruebas en dispositivos Android reales antes de publicación en Play Store.

---

## 🔄 Flujo de trabajo GitFlow

```
main
 └── dev
      └── feature/app_distribution   ← trabajo aquí
```

### Comandos Git utilizados

```bash
# 1. Crear rama desde dev
git checkout dev
git pull origin dev
git checkout -b feature/app_distribution

# 2. Trabajar y hacer commits
git add .
git commit -m "feat: configurar Firebase App Distribution"

# 3. Push y abrir Pull Request
git push origin feature/app_distribution
# → Abrir PR en GitHub: feature/app_distribution → dev

# 4. Merge a dev y luego a main
git checkout dev
git merge feature/app_distribution
git checkout main
git merge dev
git push origin main
```

---

## 🚀 Flujo de Publicación

### Generar APK → App Distribution → Testers → Instalación → Actualización

### 1. Generar APK de Release

```bash
# Versión 1.0.0
flutter build apk --release

# El APK queda en:
# build/app/outputs/flutter-apk/app-release.apk
```

### 2. Configurar Firebase App Distribution

1. Ir a [Firebase Console](https://console.firebase.google.com) → proyecto `distribucion-apk-miguel`
2. App Distribution → **Testers & Groups**
3. Crear grupo: `QA_Clase`
4. Agregar tester: `dduran@uceva.edu.co` y `miguelangelruizurmendis@gmail.com`
5. Ir a **Releases** → Subir `app-release.apk`
6. Asignar al grupo `QA_Clase`
7. Agregar Release Notes y distribuir

### 3. Actualización incremental (1.0.0 → 1.0.1)

```bash
# En pubspec.yaml cambiar:
# version: 1.0.0+1  →  version: 1.0.1+2

flutter build apk --release
# Subir nuevo APK a App Distribution
```

---

## 📦 Sección "Publicación" — Pasos para replicar en el equipo

| Paso | Acción | Comando / Herramienta |
|------|--------|-----------------------|
| 1 | Clonar repositorio | `git clone <URL>` |
| 2 | Cambiar a rama de trabajo | `git checkout feature/app_distribution` |
| 3 | Instalar dependencias | `flutter pub get` |
| 4 | Generar APK release | `flutter build apk --release` |
| 5 | Subir a App Distribution | Firebase Console → Releases |
| 6 | Agregar tester | Testers & Groups → QA_Clase |
| 7 | Distribuir y copiar enlace | Botón "Distribute" en la release |

---

## 🔢 Notas sobre Versionado

El versionado sigue el formato de Flutter: `versionName+versionCode`

| Campo | Descripción | Ejemplo |
|-------|-------------|---------|
| `versionName` | Versión visible al usuario | `1.0.1` |
| `versionCode` | Número entero incremental interno | `2` |
| En `pubspec.yaml` | Formato combinado | `version: 1.0.1+2` |

**Reglas que seguimos:**
- `versionCode` siempre sube +1 con cada build subido a App Distribution
- `versionName` sigue semver: `MAJOR.MINOR.PATCH`
- Nunca reutilizar un `versionCode` ya publicado

---

## 📝 Formato de Release Notes

```
Release v1.0.0 - [Fecha]
Responsable: Miguel Angel Ruiz Urmendis
Cambios:
- Configuración inicial del proyecto Flutter
- Integración con Firebase Analytics
- Primera distribución vía App Distribution
Credenciales de prueba: N/A (app pública)
Estado: ✅ Distribuida al grupo QA_Clase
```

---

## 📁 Estructura del proyecto

```
distribucion_apk/
├── android/
│   ├── app/
│   │   ├── build.gradle.kts     ← Firebase + applicationId
│   │   └── google-services.json ← Config Firebase (tuya)
│   └── build.gradle.kts
├── lib/
│   └── main.dart
├── pubspec.yaml                  ← version: 1.0.1+2
└── README.md
```

---

## 🐛 Bitácora de QA

Ver sección completa en el PDF de evidencias adjunto.
