# 📱 Mobile plan predictor
Modelo de clasificación para recomendar el plan óptimo (Smart o Ultra) basado en el comportamiento mensual de los usuarios.

## 📘 Descripción del proyecto
Una compañía móvil busca sustituir sus planes antiguos y necesita un modelo que recomiende el plan más adecuado para sus clientes: **Smart** o **Ultra**.  

Para lograrlo, se emplearon datos del comportamiento de usuarios que ya han migrado a los planes nuevos.  
El objetivo principal fue entrenar y evaluar un modelo de clasificación que alcance una **exactitud mínima de 0.75**.

## 🗂 Dataset
Cada registro contiene información mensual del usuario:

- `calls`: Número de llamadas realizadas  
- `minutes`: Duración total de llamadas en minutos  
- `messages`: Mensajes enviados  
- `mb_used`: Tráfico de internet consumido (MB)  
- `is_ultra`: Plan usado (1 = Ultra, 0 = Smart)

Fuente: `/datasets/users_behavior.csv`

---

## 🛠️ Proceso del proyecto
1. **Carga y exploración del dataset.**  
2. **División en conjuntos de entrenamiento, validación y prueba.**  
   - Se empleó una proporción clásica para clasificación:  
     - Train: 60%  
     - Validación: 20%  
     - Test: 20%  
3. **Entrenamiento de distintos modelos** variando hiperparámetros.  
4. **Evaluación en el conjunto de validación** para seleccionar el mejor modelo.  
5. **Prueba final en el conjunto de test.**  
6. **Prueba de cordura (sanity check)** para verificar que el modelo no solo memoriza.

---

## 🤖 Modelos evaluados
Se entrenaron distintos algoritmos probando configuraciones de hiperparámetros:

### 🔹 *Regresión Logística*
- Rápida y simple  
- **Peor desempeño en este dataset**

### 🔹 *Árbol de Decisión*
- Buen desempeño  
- Accuracy cercano al mejor modelo  
- Útil si se busca **rapidez** y fácil interpretabilidad

### 🔹 *Bosque Aleatorio (Random Forest)* – **Modelo ganador**
- Mejor exactitud general  
- Mejor manejo de variaciones en el comportamiento del usuario  
- Hiperparámetros óptimos encontrados:
  - `max_depth = 4`
  - `n_estimators = 10`

---

## 🏆 Resultados
El **Bosque Aleatorio** logró la mayor exactitud y cumplió con el umbral esperado.  
Los modelos quedaron ordenados así (de mayor a menor precisión):

1. **RandomForestClassifier** — *Mejor accuracy*
2. **DecisionTreeClassifier**
3. **LogisticRegression** — *Menor accuracy*

---

## 🧪 Prueba en el conjunto de test
El modelo seleccionado se probó en datos nunca antes vistos, confirmando su capacidad de generalización.

---

## 📝 Conclusiones
- El **Bosque Aleatorio** con `max_depth=4` y `n_estimators=10` fue el mejor modelo para este problema.  
- El **Árbol de Decisión** también obtuvo resultados altos, útil si se requiere velocidad o menor complejidad computacional.  
- La **Regresión Logística** no modeló bien las relaciones presentes en los datos.  
- El modelo cumple con los requisitos del proyecto y supera el nivel mínimo de exactitud solicitado.

---

## 📦 Tecnologías usadas
- Python  
- pandas  
- scikit-learn  
- numpy  
- matplotlib / seaborn (para exploración)
