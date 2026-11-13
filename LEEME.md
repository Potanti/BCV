# Tasa BCV: proyecto para generar el APK

## Opción A: compilar en la nube con GitHub (gratis, sin instalar nada)
1. Crea una cuenta en github.com y un repositorio nuevo (privado o público).
2. Sube TODO el contenido de esta carpeta (botón "Add file" > "Upload files").
   - Si la carpeta oculta `.github` no se sube al arrastrar, crea el archivo a mano:
     "Add file" > "Create new file", nombre `.github/workflows/build-apk.yml`,
     y pega el contenido de ese archivo.
3. Ve a la pestaña **Actions** > "Compilar APK" > **Run workflow**.
4. Espera unos 5 minutos. Al terminar, entra a la ejecución y descarga
   **tasa-bcv-apk** (abajo, en "Artifacts"). Dentro está `app-debug.apk`.
5. Pásalo al celular e instálalo (hay que permitir "instalar apps de orígenes desconocidos").

## Opción B: compilar en tu PC
Requisitos: Node 18+, Java 17 y Android Studio (con el SDK).

    npm install
    npx cap add android
    npm install --no-save @capacitor/assets && npx capacitor-assets generate --android
    npx cap sync android
    cd android && ./gradlew assembleDebug

El APK queda en `android/app/build/outputs/apk/debug/app-debug.apk`.

## Notas
- Es un APK de depuración: se instala directo, pero no sirve para Google Play.
  Para Play Store hay que firmar un APK/AAB de release.
- Las consultas de tasas usan el módulo HTTP nativo de Capacitor para evitar
  problemas de CORS dentro de la app.
