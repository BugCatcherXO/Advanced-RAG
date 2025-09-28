# 📊 Advanced RAG with Query Expansion & Visualization

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](https://www.python.org/)
[![OpenAI](https://img.shields.io/badge/OpenAI-API-green)](https://platform.openai.com/)
[![ChromaDB](https://img.shields.io/badge/Chroma-VectorDB-orange)](https://www.trychroma.com/)
[![UMAP](https://img.shields.io/badge/UMAP-Dimensionality%20Reduction-purple)](https://umap-learn.readthedocs.io/en/latest/)

Este proyecto implementa un **pipeline de Retrieval-Augmented Generation (RAG)** sobre documentos PDF.  
Integra técnicas modernas como **HyDE (Hypothetical Document Embeddings)**, **ChromaDB** y **UMAP** para:

- 📥 **Extraer** y **trocear** documentos PDF.  
- 🔎 **Indexar** fragmentos en una base vectorial.  
- 🧠 **Mejorar consultas** con respuestas hipotéticas generadas por LLM.  
- 📈 **Visualizar embeddings** en 2D para analizar qué tan efectiva es la expansión de consulta.  

---

## 🚀 Características

✅ Extracción de texto desde PDF con [`pypdf`](https://pypdf.readthedocs.io/)  
✅ Chunking avanzado con `langchain` (por caracteres + tokens)  
✅ Embeddings con [`sentence-transformers`](https://www.sbert.net/)  
✅ Almacenamiento y búsqueda en **ChromaDB**  
✅ **Query Expansion** con **HyDE** usando la API de OpenAI  
✅ Reducción de dimensionalidad con **UMAP**  
✅ Visualización interactiva de consultas, documentos recuperados y corpus  

---

## 📂 Estructura del Proyecto

```
advanced_rag/
│── venv/                           # Entorno virtual
│── data/
│   └── microsoft-annual-report.pdf # Documento de ejemplo
│── expansion_answer.py             # Script principal
│── helper_utils.py                 # Funciones auxiliares
│── .env                            # Clave de API (ignorado por git)
│── README.md                       # Este archivo
```

---

## ⚙️ Instalación

### 1. **Clonar el repo**

```bash
git clone https://github.com/tuusuario/advanced-rag.git
cd advanced-rag
```

### 2. **Crear entorno virtual**

```bash
conda create -n rag python=3.10 -y
conda activate rag
```

### 3. **Instalar dependencias**

```bash
pip install -r requirements.txt
```

**Dependencias principales:**

- openai
- pypdf
- langchain
- chromadb
- umap-learn
- matplotlib
- python-dotenv
- sentence-transformers

### 4. **Configurar variables de entorno**

Crea un archivo `.env` en la raíz del proyecto con tu clave de OpenAI:

```ini
OPENAI_API_KEY=sk-xxxxxxxxxxxxxxxx
```

---

## ▶️ Uso

Ejecuta el script principal:

```bash
python expansion_answer.py
```

El pipeline hará lo siguiente:

1. 📖 Leer y trocear el PDF de ejemplo.
2. 📦 Indexar en ChromaDB.
3. ❓ Lanzar una consulta de prueba.
4. ✨ Expandir la consulta con HyDE (respuesta hipotética).
5. 🔎 Recuperar los fragmentos más relevantes.
6. 📊 Proyectar embeddings a 2D con UMAP.
7. 🎨 Mostrar un gráfico con:
   - Corpus (gris)
   - Documentos recuperados (verde)
   - Consulta original (❌ rojo)
   - Consulta expandida (❌ naranja)

---

## 📸 Ejemplo de Visualización

- **Gris** → Todos los fragmentos del PDF
- **Verde** → Top-N fragmentos recuperados
- **Rojo X** → Consulta original
- **Naranja X** → Consulta aumentada con HyDE

---

## 🧠 Conceptos Clave

### 🔹 RAG (Retrieval-Augmented Generation)
Permite a un LLM responder preguntas usando documentos externos.
Aquí usamos ChromaDB para traer la información más relevante antes de generar una respuesta.

### 🔹 HyDE (Hypothetical Document Embeddings)
En lugar de buscar solo con la query, pedimos a un LLM que imagine una respuesta plausible.
Esa respuesta se concatena a la query → mayor similitud semántica con el corpus → mejor recuperación.

### 🔹 UMAP
Algoritmo de reducción de dimensionalidad que permite visualizar embeddings de 768D en 2D.
Sirve como herramienta de diagnóstico: si la consulta expandida está más cerca de los documentos relevantes, HyDE funcionó.

---

## 🔧 Personalización

**Cambiar documento de entrada:**

```python
reader = PdfReader("data/tu_documento.pdf")
```




---

## ⭐ Créditos

- [ChromaDB](https://www.trychroma.com/)
- [LangChain](https://www.langchain.com/)
- [UMAP-learn](https://umap-learn.readthedocs.io/en/latest/)
- [SentenceTransformers](https://www.sbert.net/)
- [OpenAI API](https://platform.openai.com/)