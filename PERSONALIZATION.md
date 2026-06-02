# Guía de Personalización — EchoVis

## 🎨 Personalizar Colores

Edita las variables CSS en la sección `:root` del archivo `index.html`:

```css
:root {
    /* Fondos */
    --bg-app: #0a0a0f;              /* Fondo negro profundo */
    --bg-surface: #111118;          /* Fondo de viewport */
    --bg-card: #1a1a24;             /* Tarjetas */
    
    /* Texto */
    --text-primary: #f0f0f0;        /* Texto principal */
    --text-secondary: #8888aa;      /* Texto secundario */
    --text-muted: #555566;          /* Texto deshabilitado */
    
    /* Acentos */
    --accent-green: #c8f135;        /* Social Space activo */
    --accent-blue: #4da6ff;         /* Modo Radar */
    --accent-yellow: #f5c842;       /* Alerta sirena */
    --accent-red: #e84040;          /* Alerta claxon */
}
```

### Ejemplos de Temas

#### Tema Claro (Light Mode)
```css
:root {
    --bg-app: #ffffff;
    --bg-surface: #f5f5f5;
    --bg-card: #e0e0e0;
    --text-primary: #000000;
    --text-secondary: #666666;
    --text-muted: #999999;
    --accent-green: #00aa00;
    --accent-blue: #0066ff;
    --accent-yellow: #ffcc00;
    --accent-red: #ff0000;
    --border-subtle: rgba(0,0,0,0.1);
    --border-card: rgba(0,0,0,0.15);
}
```

#### Tema Azul (Blue Variant)
```css
:root {
    --bg-app: #0a0a1f;
    --bg-surface: #111133;
    --bg-card: #1a1a44;
    --accent-green: #00ff88;
    --accent-blue: #00ddff;
    --accent-yellow: #ffdd00;
}
```

---

## 🔊 Personalizar Frases de Transcripción

En el archivo `index.html`, busca el array `transcriptionPhrases` (línea ~58):

```javascript
const transcriptionPhrases = [
    "Hola, ¿cómo estás hoy?",
    "Ese fue un sonido muy interesante",
    "Puedo escuchar las aves afuera",
    "¿Oíste ese ruido en la calle?",
    "La música está sonando bastante fuerte",
    "Qué día más tranquilo"
];
```

**Personaliza** con tus propias frases:

```javascript
const transcriptionPhrases = [
    "Detectado: Voz masculina",
    "Detectado: Conversación en español",
    "Detectado: Música de fondo",
    "Detectado: Ruido de tráfico",
    "Detectado: Timbre de puerta",
    "Detectado: Aplicación ejecutándose"
];
```

---

## 🎙️ Ajustar Parámetros de Audio

### FFT Size (Análisis de Frecuencia)
En `initializeAudio()`, línea ~90:

```javascript
state.analyser.fftSize = 256;  /* 256, 512, 1024, 2048 */
```

- **256**: Resolución baja, mejor para tiempo real
- **512**: Balance
- **1024+**: Resolución alta, más latencia

### Duración de Bloques de Grabación
En `startRecordingCycle()`, línea ~114:

```javascript
setTimeout(() => {
    state.mediaRecorder.stop();
}, 3000);  /* 3000ms = 3 segundos */
```

Cambiar a (ej. 2 segundos):
```javascript
}, 2000);
```

### Latencia de Procesamiento
En `handleAudioBlock()`, línea ~137:

```javascript
setTimeout(() => {
    // ... procesar audio
}, 800);  /* 800ms de latencia simulada */
```

Cambiar a (ej. 500ms):
```javascript
}, 500);
```

---

## 📊 Ajustar Umbrales de Alerta (dB)

En `monitorNoiseLevel()`, línea ~174:

```javascript
if (state.currentDB > 75) {  /* Umbral para alerta */
```

En `updateRadarMeter()`, línea ~192:

```javascript
if (dB >= 95) {
    statusText = '🔴 PELIGRO';
} else if (dB >= 80) {
    statusText = '🟡 NIVEL ALTO';
}
```

### Recomendaciones:
- **< 60 dB**: Entorno muy tranquilo (susurros)
- **60-75 dB**: Conversación normal
- **75-85 dB**: Nivel elevado (TV, música)
- **≥ 85 dB**: Riesgo auditivo a largo plazo

---

## 🎨 Personalizar Animaciones

### Velocidad de Pulse del Micrófono
En CSS, línea ~52:

```css
.mic-indicator {
    animation: pulse 1.5s infinite;  /* 1.5s = duración */
}
```

Cambiar a (ej. 1s para más rápido):
```css
animation: pulse 1s infinite;
```

### Velocidad de Emojis Flotantes
En CSS, línea ~153:

```css
@keyframes floatUp {
    /* ... */
    animation: floatUp 1.2s ease-out forwards;
}
```

### Duración de Destellos de Alerta
En CSS, línea ~169:

```css
@keyframes flashYellow {
    /* ... duración 300ms ... */
}
```

---

## 📱 Ajustar Dimensiones del Viewport

En CSS (media query desktop), línea ~117:

```css
@media (min-width: 481px) {
    #app-viewport {
        max-width: 390px;    /* Ancho */
        height: 844px;       /* Alto */
        border-radius: 24px; /* Redondeo de esquinas */
        box-shadow: 0 0 60px rgba(0, 0, 0, 0.8);
    }
}
```

**Ejemplos**:
- iPhone SE (2020): 390px × 667px
- iPhone 14: 390px × 844px
- iPad Mini: 768px × 1024px

---

## 🔔 Personalizar Mensajes de Notificación

En `showAlert()`, línea ~1100:

```javascript
function showAlert(message, isDanger = false) {
    const notification = DOM.alertNotification;
    notification.textContent = message;
    // ...
}
```

Los mensajes se generan en:
- Línea ~173: `showAlert('⚠️ Nivel elevado detectado', false);`
- Línea ~217: `showAlert('⚠️ SIRENA DE EMERGENCIA DETECTADA', false);`
- Línea ~231: `showAlert('🚗 CLAXON DE AUTO — VEHÍCULO CERCA', true);`

Cambiar a (ej. español técnico):
```javascript
showAlert('🔊 Nivel de ruido muy alto detectado', false);
showAlert('🚨 Alerta: Sirena activada', false);
showAlert('⚠️ Peligro: Auto a proximidad', true);
```

---

## 🎯 Integración Real con Whisper API (TODO)

Actualmente, el código simula transcripción con frases predefinidas.

Para integración real con OpenAI Whisper:

```javascript
async function handleAudioBlock(audioData) {
    showProcessingIndicator();

    try {
        const formData = new FormData();
        formData.append('file', new Blob([audioData], { type: 'audio/webm' }), 'audio.webm');
        formData.append('model', 'whisper-1');
        formData.append('language', 'es');

        const response = await fetch('https://api.openai.com/v1/audio/transcriptions', {
            method: 'POST',
            headers: {
                'Authorization': `Bearer YOUR_API_KEY`
            },
            body: formData
        });

        const result = await response.json();
        removeProcessingIndicator();
        
        if (result.text) {
            addTranscriptionBubble(result.text);
        }
    } catch (error) {
        console.error('Error en transcripción:', error);
        removeProcessingIndicator();
    }
}
```

**Nota**: Requiere API key y CORS habilitado.

---

## 🛠️ Debugging

### Habilitar logs en consola
Abre DevTools (F12) y verifica la consola para:
- Acceso de micrófono
- Cambios de estado de dB
- Eventos de grabación

### Verificar soporte de MediaRecorder
```javascript
console.log(MediaRecorder.isTypeSupported('audio/webm'));
console.log(MediaRecorder.isTypeSupported('audio/ogg'));
```

### Monitorear dB en tiempo real
En `monitorNoiseLevel()`, añade después de la línea 173:
```javascript
console.log(`DB: ${state.currentDB}`);
```

---

## 📦 Exportar Grabaciones de Audio

Para guardar los bloques de audio capturados:

```javascript
function handleAudioBlock(audioData) {
    // Crear Blob URL para descarga
    const url = URL.createObjectURL(audioData);
    const a = document.createElement('a');
    a.href = url;
    a.download = `audio_${Date.now()}.webm`;
    // a.click();  // Descomentar para auto-descargar
    
    // ... resto del código
}
```

---

## 🚀 Deployment

### Servir con Python 3
```bash
python -m http.server 8000
```

### Servir con Node.js
```bash
npx http-server
```

### Compartir online (GitHub Pages)
1. Sube `index.html` a un repositorio GitHub
2. Habilita GitHub Pages en Settings
3. Accede a `https://username.github.io/repository/index.html`

---

**¡Diviértete personalizando EchoVis!** 🚀

