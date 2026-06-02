# 🚀 EchoVis v3 — Despliegue en Vercel

## ¿Por qué Vercel y no localhost?

**Web Speech API requiere:**
- ✅ HTTPS (seguridad)
- ✅ Conexión a internet (para contactar Google)
- ✅ Servidor en línea

**Localhost sin internet no funciona** porque Web Speech API necesita conectarse a `https://www.google.com/speech-api/` para procesar el audio.

---

## 📋 Pasos para Desplegar

### **Opción 1: Despliegue automático (RECOMENDADO)**

#### 1. Sube el código a GitHub
```bash
git init
git add .
git commit -m "EchoVis v3 - Web Speech API"
git remote add origin https://github.com/TU_USUARIO/echovis.git
git push -u origin main
```

#### 2. Conecta Vercel a tu repositorio
1. Ve a https://vercel.com
2. Haz clic en "New Project"
3. Selecciona tu repositorio de GitHub
4. Haz clic en "Deploy"

**¡Listo!** Vercel detectará automáticamente que es HTML estático y lo despliegará.

---

### **Opción 2: Despliegue manual (SIN GitHub)**

#### 1. Instala Vercel CLI
```bash
npm install -g vercel
```

#### 2. Desde la carpeta del proyecto
```bash
cd C:\Users\ERICK CAICEDO\IdeaProjects\untitled1
vercel
```

Sigue las instrucciones interactivas. **¡Listo!**

---

## ✅ Qué Pasará Después del Despliegue

Una vez desplegado en Vercel:
1. Recibirás una URL como: `https://echovis.vercel.app/`
2. Abre esa URL en Chrome/Edge
3. **Permite el micrófono cuando lo pida**
4. **Habla cerca del micrófono**
5. ✅ Las burbujas de transcripción aparecerán en tiempo real

---

## 🔍 Verificar que Funciona

Después de desplegar, abre DevTools (F12) y verifica:

```javascript
// En la consola, deberías ver:
🎙️ Web Speech API activado - ESPERA A QUE APAREZCA UNA BURBUJA GRIS MIENTRAS HABLAS
📊 Resultados recibidos: 1
  ○ interim (85%): "hol..."
  ✓ FINAL (92%): "hola"
```

---

## 🌐 URLs Útiles

- **Vercel Dashboard**: https://vercel.com/dashboard
- **Docs Vercel**: https://vercel.com/docs
- **Web Speech API**: https://developer.mozilla.org/es/docs/Web/API/Web_Speech_API

---

## ⚡ Ventajas de Vercel

| Aspecto | Localhost | Vercel |
|--------|-----------|--------|
| Web Speech API | ❌ No funciona (sin internet) | ✅ Funciona (HTTPS + internet) |
| Acceso público | ❌ Solo local | ✅ URL mundial |
| SSL/HTTPS | ❌ No | ✅ Automático |
| Costo | Gratis | Gratis (plan hobby) |
| Deploy | Manual | Automático (git push) |

---

## 📱 Después del Despliegue

Comparte la URL de Vercel con cualquier persona y podrá usar EchoVis en cualquier navegador:
```
https://echovis.vercel.app/index.html
```

---

**¿Necesitas ayuda con el despliegue? Abre GitHub y comparte el link cuando esté hecho.** 🚀

