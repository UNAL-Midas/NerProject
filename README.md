# Legal NER Colombia – Contratos Públicos

> Conjunto de datos creado a partir de 286 contratos públicos en Colombia, ideal para entrenar modelos del dominio legal con reconocimiento de entidades de granularidad fina.

---

## Tabla de contenidos

- [Información general](#información-general)
- [Tecnologías usadas](#tecnologías-usadas)
- [Funcionalidades](#funcionalidades)
- [Configuración](#configuración)
- [Implementación](#implementación)
- [Estatus del proyecto](#estatus-del-proyecto)
- [Agradecimientos](#agradecimientos)
- [Contacto](#contacto)

---

## Información general

Este modelo de **Named Entity Recognition (NER)** permite reconocer entidades de granularidad fina en textos legales.

Su propósito es identificar partes relevantes dentro de contratos públicos en Colombia, facilitando el análisis automatizado de documentos jurídicos.

---

## Tecnologías usadas

- Python  
- TensorFlow  
- Keras  

---

## Funcionalidades

- Entrenamiento con validación cruzada  
- Modelo NER basado en arquitectura BiLSTM  
- Reconocimiento de entidades jurídicas de dominio específico  

---

## Configuración

Los modelos fueron creados utilizando aprendizaje profundo con la API de **Keras**.

Para su correcta carga o despliegue es necesario:

- Cargar el archivo del modelo con extensión `.keras`
- Cargar los diccionarios de tokens y entidades (`word2idx.pkl` y `entity2idx.pkl`)
- Reconstruir el diccionario inverso `idx2entity`

---

## Implementación

### Ejemplo de carga del modelo en una aplicación web

```python
import tensorflow as tf

_model = None

def load_model():
    global _model
    if _model is None:
        print("Cargando modelo NER...")
        _model = tf.keras.models.load_model(
            "app/models/ner_model/modelo_bilstm_cross_fold9.keras"
        )
        print("Modelo cargado correctamente")
    return _model
```

---

### Ejemplo de carga del modelo y diccionarios

```python
import tensorflow as tf
import pickle
import os

ruta_modelo = "/content/drive/MyDrive/NER tesis/Modelos/propiorNERcross"

# Cargar modelo entrenado (fold 9 como ejemplo)
modelo = tf.keras.models.load_model(
    os.path.join(ruta_modelo, "modelo_bilstm_cross_fold9.keras")
)

# Cargar diccionarios
with open(os.path.join(ruta_modelo, "word2idx.pkl"), "rb") as f:
    word2idx = pickle.load(f)

with open(os.path.join(ruta_modelo, "entity2idx.pkl"), "rb") as f:
    entity2idx = pickle.load(f)

# Diccionario inverso
idx2entity = {i: e for e, i in entity2idx.items()}
```

---

## Despliegue en la nube

En caso de requerir el modelo en la nube, puede utilizarse Firebase Hosting para exponer el modelo y realizar llamadas desde una aplicación web o móvil.

---

## Estatus del proyecto

Proyecto finalizado, sujeto a recomendaciones académicas.

---

## Agradecimientos

Universidad Nacional de Colombia  
Grupo de investigación MIDAS  

---

## Contacto

Viviana Sofia Murillo Sossa  
vsmurillos@unal.edu.co  
sofimurillosos@gmail.com  
