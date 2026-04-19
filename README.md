# Laboratorio 6 — Sistemas y Tecnologías Web

**Curso:** Sistemas y Tecnologías Web  
**Docente:** Marlon Fuentes  
**Semestre:** 1, 2026

---

## Parte 1: Corrección de `servidor-malo.js`

### Bug 1 — Paréntesis de cierre faltantes

**Problema:** `http.createServer(...)` y `server.listen(...)` no tenían su paréntesis de cierre, causando un `SyntaxError` al intentar ejecutar el archivo.

**Corrección:**
```js
const server = http.createServer(async (req, res) => {
  // ...
})

server.listen(PORT, () => {
  console.log(`Servidor corriendo en http://localhost:${PORT}`)
})
```

---

### Bug 2 — Content-Type incorrecto en `/info`

**Problema:** El header usaba `"application-json"` con guión en lugar de `"application/json"` con slash.

**Corrección:**
```js
res.writeHead(200, { "Content-Type": "application/json" })
```

---

### Bug 3 — `await` faltante en `fs.readFile`

**Problema:** Sin `await`, la variable `texto` contenía una `Promise` en lugar del contenido del archivo. Al serializar con `JSON.stringify` se obtenía `{}`.

**Corrección:**
```js
const texto = await fs.readFile(filePath, "utf-8")
```

---

### Bug 4 — Status code 200 en respuesta 404

**Problema:** La ruta de "no encontrado" respondía con `200 OK`, lo cual es semánticamente incorrecto.

**Corrección:**
```js
res.writeHead(404, { "Content-Type": "text/plain" })
```

---

## Parte 2: Nuevas funcionalidades

### `/info` responde JSON

Ahora retorna un objeto con `mensaje`, `curso` y `tecnologia`.

### Nueva ruta `/saludo`

Responde con texto plano un mensaje de bienvenida.

### Nueva ruta `/api/status`

Responde un JSON con `ok`, `status` y `puerto`.

### 404 muestra la ruta intentada

```js
res.end(`Ruta no encontrada: ${req.url}`)
```
