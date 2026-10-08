# hola-Mundo
# 🧭 Pauta reto 1: Pegad aquí los enlaces de vuestro hola mundo y comprobad el formato
repo_url = ""   # Ej: "https://github.com/tu-usuario/hola-ia"
app_url  = ""   # Ej: "https://hola-ia-tu-nombre.streamlit.app" (ruta A) o "https://tu-usuario-hola-ia.hf.space" (ruta B)

from urllib.parse import urlparse

def comprobar_repo(url):
    u = urlparse(url.strip())
    partes = [p for p in u.path.split("/") if p]
    if u.scheme != "https" or u.netloc.removeprefix("www.") not in ("github.com",):
        return "❌ Debe ser una URL https de github.com"
    if len(partes) < 2:
        return "❌ Falta la ruta completa del repositorio (usuario y nombre del repositorio)"
    return "✅ Formato correcto"

def comprobar_app(url):
    u = urlparse(url.strip())
    if u.netloc.endswith(".gradio.live"):
        return "❌ Los enlaces share de Gradio caducan en una semana y no cuentan como despliegue"
    if u.scheme != "https" or not u.netloc.endswith((".streamlit.app", ".hf.space")):
        return "❌ Debe ser https://<nombre>.streamlit.app (ruta A) o https://<usuario>-<space>.hf.space (ruta B)"
    return "✅ Formato correcto"

print(f"Repositorio: {repo_url or '(vacío)'} → {comprobar_repo(repo_url)}")
print(f"App:         {app_url or '(vacío)'} → {comprobar_app(app_url)}")
print("\n⚠️ El formato no basta: abrid cada enlace en una ventana de incógnito para comprobar que es público y que la app carga.")
