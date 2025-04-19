# 📱 Vulnerabilidad Crítica: Permisos Excesivos y Riesgo de Grabación de Audio No Autorizada en la App de Criptomonedas `com.cryptology.flutter`

## 🔐 Descripción de la Vulnerabilidad

Se han identificado múltiples **vulnerabilidades críticas** en la aplicación móvil `com.cryptology.flutter`, una app de criptomonedas disponible para Android. Estas vulnerabilidades representan un riesgo grave para la **privacidad** y **seguridad de los usuarios**, principalmente debido a:

- Solicitud excesiva de permisos no justificados.
- Acceso continuo al micrófono mediante el permiso `FOREGROUNDSERVICEMICROPHONE`.
- Acceso al micrófono en tiempo de ejecución sin consentimiento explícito del usuario.

---

## 🚨 1. Permisos Excesivos

La aplicación solicita una serie de permisos que **no están directamente relacionados con su funcionalidad principal** como app de intercambio de criptomonedas:

- `READ_EXTERNAL_STORAGE`
- `WRITE_EXTERNAL_STORAGE`
- `CAMERA`
- `ACCESS_FINE_LOCATION`
- `ACCESS_COARSE_LOCATION`
- `WRITE_SETTINGS`
- `FOREGROUNDSERVICE_MICROPHONE` (📢 permite grabación continua de audio en segundo plano)

Estos permisos representan una grave amenaza a la privacidad de los usuarios, abriendo la posibilidad a la recolección masiva de datos sensibles y vigilancia encubierta.

---

## ⚙️ 2. Permisos Concedidos Durante la Instalación

Durante la instalación, se otorgan automáticamente varios permisos sensibles, sin intervención del usuario:

```plaintext
android.permission.FOREGROUNDSERVICEMICROPHONE: granted=true
android.permission.RECORD_AUDIO: granted at runtime (ver sección 3)
android.permission.INTERNET: granted=true
android.permission.ACCESS_NETWORK_STATE: granted=true
android.permission.USE_FINGERPRINT: granted=true
android.permission.USE_BIOMETRIC: granted=true
android.permission.ACCESS_WIFI_STATE: granted=true
android.permission.RECEIVE_BOOT_COMPLETED: granted=true
com.google.android.gms.permission.AD_ID: granted=true

El permiso FOREGROUNDSERVICEMICROPHONE es particularmente preocupante porque permite la grabación continua de audio incluso cuando la app está en segundo plano, sin necesidad de interacción adicional por parte del usuario.

🎙️ 3. Permiso RECORD_AUDIO en Tiempo de Ejecución
Durante pruebas en un dispositivo Samsung A52, se confirmó que la app tiene habilitado el permiso RECORD_AUDIO, sin mostrar ninguna solicitud al usuario para activarlo:

Dispositivo de prueba: Samsung A52

Permiso: android.permission.RECORD_AUDIO: granted=true

Observación: En ningún momento se solicitó acceso al micrófono explícitamente al usuario.

⚠️ Esto representa una grave violación de la privacidad, y puede estar infringiendo leyes de protección de datos, como el GDPR en Europa.

⚖️ Consideraciones Legales
La grabación y procesamiento de datos de audio sin consentimiento explícito del usuario puede violar múltiples normativas:

Reglamento General de Protección de Datos (GDPR) – Unión Europea

Leyes nacionales sobre privacidad de las comunicaciones

Leyes de consentimiento para grabaciones (dependiendo de la jurisdicción)

Incluso si el propósito fuera marketing, es obligatorio informar y obtener consentimiento claro y específico del usuario.

🧪 Pasos de Validación
🔍 Análisis del APK
Descargar el APK:
https://apkcombo.app/en/tothemoon-buy-trade-btc/com.cryptology.flutter/download/apk

Descompilar el APK con apktool:

bash
Copiar
Editar
apktool d com.cryptology.flutter.apk -o decrypted_apk
Revisar AndroidManifest.xml para verificar los permisos solicitados.

📱 Pruebas en Dispositivo
Instalar la app en un Samsung A52.

Conectar el dispositivo vía ADB:

bash
Copiar
Editar
adb devices
adb shell getprop ro.product.manufacturer
adb shell getprop ro.product.model
Verificar permisos otorgados:

bash
Copiar
Editar
adb shell dumpsys package com.cryptology.flutter | grep permission
Confirmar que no se solicita acceso al micrófono de forma explícita durante la instalación o ejecución.

💥 Impacto

Riesgo	Descripción
🕵️‍♂️ Violación de Privacidad	Grabación de conversaciones sin consentimiento
💸 Robo de Datos Financieros	Acceso potencial a información de wallets y cuentas
🧬 Manipulación de Datos	Modificación de configuraciones sin conocimiento del usuario
🧠 Recolección de Datos Personales	Uso para marketing o fines no revelados
⚠️ Compromiso Total del Dispositivo	Uso malicioso de sensores y hardware
🔎 Clasificación de la Vulnerabilidad (CVSS)
Gravedad: CRÍTICA

Vector de Ataque: RED

Complejidad del Ataque: BAJA

Privilegios Requeridos: NINGUNO

Interacción del Usuario: NINGUNA

Ámbito Afectado: CAMBIADO

Confidencialidad: ALTA

Integridad: ALTA

Disponibilidad: BAJA

🛡️ Recomendaciones
Eliminar permisos innecesarios del AndroidManifest.xml.

Solicitar permisos sensibles (como micrófono o ubicación) solo cuando sea estrictamente necesario y con consentimiento explícito.

Implementar transparencia en políticas de privacidad y flujo de consentimiento.

Auditoría externa de seguridad y cumplimiento de privacidad.

Cumplimiento estricto del GDPR y regulaciones locales sobre grabación y tratamiento de datos personales.

📌 Conclusión
La aplicación com.cryptology.flutter representa un riesgo severo a la privacidad y seguridad del usuario, especialmente por su capacidad de grabar audio sin consentimiento. Se recomienda enfáticamente realizar una revisión exhaustiva del código, ajustar los permisos solicitados, y asegurar cumplimiento con todas las normativas de protección de datos antes de continuar su distribución.
