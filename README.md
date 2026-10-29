# Dashboard de Gastos

Dashboard personal de gastos desplegable en **Render.com** (gratis, desde GitHub).

---

## 🚀 Deploy en Render.com (recomendado)

### 1. Sube el proyecto a GitHub

```bash
git init
git add .
git commit -m "init dashboard gastos"
git remote add origin https://github.com/TU_USUARIO/TU_REPO.git
git push -u origin main
```

### 2. Crea el servicio en Render

1. Ve a [render.com](https://render.com) → **New → Web Service**
2. Conecta tu cuenta de GitHub y elige el repo
3. Render detecta `render.yaml` automáticamente — pulsa **Deploy**
4. En ~2 min tienes una URL pública tipo `https://dashboard-gastos-xxxx.onrender.com`

### 3. Configura la persistencia de datos (importante)

Para que los datos no se pierdan cuando Render reinicia el servidor, configura estas variables de entorno en **Render → Environment**:

| Variable | Valor |
|---|---|
| `GITHUB_TOKEN` | Tu [Personal Access Token](https://github.com/settings/tokens) con permiso `repo` |
| `GITHUB_REPO` | `tu-usuario/tu-repo` |
| `GITHUB_BRANCH` | `main` |

Con esto, cada vez que subas un Excel el servidor guarda los datos localmente **y** hace un commit automático a tu repo. Si Render reinicia, descarga los datos actualizados de GitHub.

---

## 💻 Uso local

```bash
pip install -r requirements.txt
python app.py
# Abre http://localhost:8000
```

---

## 📤 Actualizar gastos

Desde la web: botón **⬆ Cargar Excel** (cabecera). Arrastra tu Excel → los datos se actualizan al instante sin recargar la página.

---

## 📁 Estructura

```
gastos_app/
├── app.py              ← FastAPI backend
├── render.yaml         ← Config para Render.com
├── requirements.txt
├── .gitignore
├── README.md
├── data/
│   └── gastos.json     ← Datos (803 registros iniciales)
└── static/
    └── index.html      ← Dashboard (Resumen / Comparativa / Evolución / Consejos)
```

---

## ⚠️ Nota sobre el tier gratuito de Render

El plan gratuito hace que el servidor **duerma** tras 15 min de inactividad. La primera visita tras la inactividad tarda ~30 segundos en arrancar (cold start). Para uso personal esto es perfectamente válido.
