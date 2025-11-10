# Udemy Neo4j Dataset

Este repositorio contiene un conjunto completo de archivos CSV diseñados para poblar una base de datos **Neo4j** que simula una plataforma de cursos en línea tipo *Udemy*.  
La información está estructurada de forma jerárquica y coherente para permitir el análisis y la exploración mediante consultas Cypher.

---

## 🧩 Estructura general del dataset

El dataset está compuesto por **7 grafos principales (nodos)** y **9 tipos de relaciones**, todos interconectados y coherentes entre sí.  
Las relaciones utilizan el prefijo `id` para los identificadores, lo que facilita su distinción respecto a otras propiedades.

---

## 🧱 Nodos

| Archivo | Descripción | Cantidad |
|----------|--------------|-----------|
| **usuarios.csv** | Datos de 20 usuarios con nombre, edad, sexo, correo y fecha de nacimiento. | 20 |
| **cursos.csv** | 20 cursos sobre programación, ciencia de datos, desarrollo web y ciberseguridad, con nivel, año de publicación y calificación promedio. | 20 |
| **categorias.csv** | 4 categorías principales que agrupan los cursos por temática. | 4 |
| **idiomas.csv** | 4 idiomas disponibles para los cursos. | 4 |
| **paises.csv** | 4 países en los que se ofrecen los cursos. | 4 |
| **modulos.csv** | Módulos que componen cada curso (3–4 por curso). | 68 |
| **lecciones.csv** | Lecciones dentro de cada módulo (3–4 por módulo). | 231 |

---

## 🔗 Relaciones

| Archivo | Descripción | Detalles clave |
|----------|--------------|----------------|
| **esta_compuesto.csv** | Relación `(:Curso)-[:ESTA_COMPUESTO]->(:Modulo)` | Cada curso está compuesto por 3–4 módulos. |
| **contiene.csv** | Relación `(:Modulo)-[:CONTIENE]->(:Leccion)` | Cada módulo contiene 3–4 lecciones. |
| **disponible_en.csv** | Relación `(:Curso)-[:DISPONIBLE_EN]->(:Pais)` | Cada curso se ofrece en 2–4 países, y **al menos una relación incluye una fecha de finalización (`fechaFin`)**. |
| **inscrito_en.csv** | Relación `(:Usuario)-[:INSCRITO_EN]->(:Curso)` | Cada usuario está inscrito en 4–7 cursos, con progreso y estado coherentes. Si `progreso=100`, el curso se marca como `Completado` y posee `fechaFin`. |
| **le_gusta.csv** | Relación `(:Usuario)-[:LE_GUSTA]->(:Curso)` | Representa valoraciones (1–5) que los usuarios otorgan a cursos. |
| **vio.csv** | Relación `(:Usuario)-[:VIO]->(:Leccion)` | Los usuarios que completaron un curso han visto **todas las lecciones** del mismo, con `finalizado=true` y duración completa. |
| **pertenece_a.csv** | Relación `(:Curso)-[:PERTENECE_A]->(:Categoria)` | Cada curso pertenece a una categoría específica. |
| **reside_en.csv** | Relación `(:Usuario)-[:RESIDE_EN]->(:Pais)` | Cada usuario reside en un país. |
| **en_idioma.csv** | Relación `(:Curso)-[:EN_IDIOMA]->(:Idioma)` | Cada curso está asociado a un idioma principal. |

---

## ⚙️ Coherencia de los datos

La versión **v5** incluye mejoras significativas respecto a versiones anteriores:

- **Fechas realistas:**  
  En `disponible_en.csv`, todos los cursos tienen al menos una relación con `fechaFin` no vacía.

- **Progreso y estados coherentes:**  
  En `inscrito_en.csv`:
  - Si `progreso = 100`, entonces `estado = "Completado"` y `fechaFin` está definida.  
  - Si `estado = "Completado"`, entonces `progreso = 100`.  
  - Cursos en progreso o abandonados presentan valores intermedios.

- **Visualización completa de lecciones:**  
  En `vio.csv`, los usuarios que completaron un curso han visto todas sus lecciones con `finalizado=true` y `minutosReproducidos` igual a la duración total de cada lección.

- **Consistencia jerárquica:**  
  Los módulos y lecciones son únicos por curso y módulo, sin reutilización ni solapamiento.

---

## 🏷️ Créditos

**Versión:** v5 (2025)  
**Autor:** Generado automáticamente por *ChatGPT (GPT-5)*  
**Uso:** Académico y educativo — libre de derechos para propósitos de aprendizaje.

---
