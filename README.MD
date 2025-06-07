## 📘 API de Comentarios

Esta API permite gestionar comentarios de usuarios mediante solicitudes **GET** y **POST**.

### 🌍 **Base URL**
```
http://127.0.0.1:8000/comment/
```

### 🏗️ **Endpoints**

### 🔹 `GET /comment/`
**Descripción:** Obtiene todos los comentarios registrados.  
**Ejemplo de solicitud:**
```bash
curl -X GET http://127.0.0.1:8000/comment/
```
**Respuesta esperada (JSON):**
```json
[
    {
        "id": 1,
        "user": "Pedro",
        "comment": "¡Esto es genial!"
    },
    {
        "id": 2,
        "user": "Ana",
        "comment": "Gracias por la información."
    }
]
```

### 🔹 `POST /comment/`
**Descripción:** Envía un nuevo comentario.  
**Requiere:** Datos en formato JSON y autenticación CSRF.  
**Parámetros:**  
| Parámetro | Tipo   | Obligatorio | Descripción            |
|-----------|--------|-------------|------------------------|
| `user`    | string | ✅          | Nombre del usuario    |
| `comment` | string | ✅          | Texto del comentario  |

**Ejemplo de solicitud:**
```bash
curl -X POST http://127.0.0.1:8000/comment/ \
     -H "Content-Type: application/json" \
     -H "X-CSRFToken: {TOKEN_AQUI}" \
     --data '{
        "user": "Roybel",
        "comment": "¡Excelente API!"
     }'
```

**Respuesta esperada (JSON):**
```json
{
    "status": "success",
    "username": "Roybel",
    "comment": "¡Excelente API!"
}
```

### 🔹 **Métodos no permitidos**
Si se intenta acceder con un método distinto a `GET` o `POST`, la API responderá con:
```json
{
    "error": "Metodo no permitido"
}
```
Código de respuesta: `405 - Method Not Allowed`

### 🔐 **Seguridad y CSRF**
Para proteger contra ataques **CSRF**, la API requiere que las solicitudes **POST** incluyan el token CSRF en el encabezado:
```markdown
X-CSRFToken: {TOKEN_AQUI}
```
Las cookies deben enviarse junto con las solicitudes usando `credentials: 'include'` en el frontend.

### 🚀 **Errores comunes**
| Código | Descripción |
|--------|------------|
| 400    | Falta `user` o `comment` en la solicitud |
| 403    | CSRF no validado |
| 405    | Método no permitido |
| 500    | Error interno del servidor |

---

Esta documentación deja clara la funcionalidad de tu API y asegura que cualquiera pueda usarla sin tropezar con detalles ocultos. ¿Quieres agregar algo más, como autenticación o validaciones adicionales? 😃🔥

