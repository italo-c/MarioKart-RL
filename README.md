# 🏎️ Deep Reinforcement Learning for Autonomous Driving in Super Mario Kart

## DQN vs DDQN for Autonomous Racing in Super Mario Kart (SNES)

Este proyecto explora la aplicación de **Aprendizaje por Refuerzo Profundo (Deep Reinforcement Learning)** para desarrollar un agente capaz de conducir de manera autónoma en el videojuego **Super Mario Kart (SNES)**.

El objetivo principal es comparar el desempeño de dos algoritmos basados en valor:

* 🧠 Deep Q-Network (DQN)
* 🧠 Double Deep Q-Network (DDQN)

La investigación evalúa su capacidad para aprender políticas de conducción eficientes mediante observaciones visuales, optimizando velocidad, progreso en la pista y estabilidad de conducción.

---

## 🎯 Objetivos

### Objetivo General

Desarrollar y comparar agentes basados en DQN y DDQN para la conducción autónoma en Super Mario Kart.

### Objetivos Específicos

* Implementar procesamiento visual mediante imágenes en escala de grises de 84×84 píxeles.
* Diseñar una función de recompensa basada en velocidad, progreso y permanencia en pista.
* Comparar DQN y DDQN utilizando métricas de retorno acumulado y tiempo de entrenamiento.
* Analizar el impacto de hiperparámetros como:

  * Replay Memory Size
  * Epsilon Decay
  * Reward Shaping

---

## 🎮 Entorno de Simulación

El entorno fue implementado utilizando:

* Stable-Retro
* Gymnasium
* Google Colaboratory
* Super Mario Kart (SNES)

La interacción se realiza mediante observaciones visuales extraídas directamente del emulador.

### Estado del Agente

Cada estado está compuesto por:

* 4 frames consecutivos
* Escala de grises
* Resolución 84×84

Dimensión final:

```text
(4, 84, 84)
```

---

## 🖼️ Pipeline de Procesamiento

```text
Frame RGB
    ↓
Escala de grises
    ↓
Redimensionamiento 84x84
    ↓
Normalización [0,1]
    ↓
Stack de 4 frames
    ↓
CNN
    ↓
Valores Q
```

---

## 🧠 Algoritmos Implementados

### Deep Q-Network (DQN)

Implementación base utilizando:

* Experience Replay
* Target Network
* Política ε-greedy
* Frame Skipping

### Double Deep Q-Network (DDQN)

Extensión de DQN diseñada para reducir el sesgo de sobreestimación de valores Q mediante:

* Selección de acción con Online Network
* Evaluación de acción con Target Network

---

## 🏗️ Arquitectura de la Red Neuronal

La arquitectura utilizada sigue el enfoque clásico de DeepMind para videojuegos tipo Atari:

* Capas convolucionales (CNN)
* Extracción automática de características visuales
* Capas densas fully connected
* Salida con valores Q para cada acción disponible

---

## 🎯 Reward Shaping

Uno de los principales aportes del proyecto fue el diseño de una función de recompensa personalizada para evitar problemas de reward hacking observados con la recompensa original.

### Componentes de la recompensa

#### 🚀 Speed Reward

Incentiva velocidades altas y penaliza movimientos incorrectos.

#### 🏁 Checkpoint Reward

Recompensa el progreso a lo largo del circuito.

#### 🛣️ Track Reward

Premia mantenerse dentro de la pista y penaliza colisiones o salidas.

---

## ⚙️ Configuración Experimental

| Parámetro           | Valor     |
| ------------------- | --------- |
| Episodios           | 300       |
| Learning Rate       | 1e-4      |
| Discount Factor (γ) | 0.99      |
| Batch Size          | 64        |
| Replay Memory       | 8000      |
| Epsilon Start       | 1.0       |
| Epsilon Min         | 0.01      |
| Target Update       | 200 pasos |

---

## 📊 Experimentos Realizados

### Comparación DQN vs DDQN

Se evaluó:

* Retorno acumulado
* Estabilidad del aprendizaje
* Tiempo de entrenamiento

### Reward Function

Comparación entre:

* Recompensa original del entorno
* Recompensa personalizada

### Replay Memory

Valores evaluados:

```text
1000
8000
25000
```

### Epsilon Decay

Valores evaluados:

```text
5000
10000
20000
```

---

## 📈 Resultados Principales

### DQN vs DDQN

| Métrica                       | DQN     | DDQN   |
| ----------------------------- | ------- | ------ |
| Tiempo de entrenamiento (s)   | 2837    | 3031   |
| Retorno máximo                | 1362.20 | 572.50 |
| Promedio últimos 20 episodios | 563.54  | -69.58 |

Bajo la configuración evaluada, **DQN obtuvo mejores resultados globales que DDQN**, alcanzando mayores retornos y una tendencia de aprendizaje más consistente.

---

## 🔍 Hallazgos

* El diseño de la función de recompensa tuvo mayor impacto que la elección entre DQN y DDQN.
* Un replay memory intermedio (8000) ofreció el mejor equilibrio entre diversidad y relevancia temporal.
* Un epsilon decay de 10000 permitió balancear adecuadamente exploración y explotación.
* DDQN no superó a DQN bajo la configuración experimental utilizada.

---

## 🚀 Trabajo Futuro

* Implementar Reward Shaping basado en potencial.
* Incorporar información de trayectoria y orientación.
* Migrar hacia algoritmos Actor-Critic:

  * A2C
  * PPO
  * SAC
* Explorar espacios de acción continuos.
* Transferir el agente a simuladores de conducción más realistas.

---

## 👥 Autores

* Italo Marcelo Carrión Segura
* Rodrigo Alejandro Holguín Huari
* Cristian Smith Calderón Barrial
* Oscar Sebastián Céspedes Vásquez
* Santiago Yábar Reaño

---

## 🎓 Curso

Aprendizaje por Refuerzo (1INF60)

Pontificia Universidad Católica del Perú (PUCP)

---

## 📚 Referencias

El proyecto se basa en trabajos recientes sobre:

* Deep Reinforcement Learning
* Autonomous Driving
* Deep Q-Networks
* Double Deep Q-Networks
* Atari Learning Framework

Las referencias completas pueden consultarse en el informe académico incluido en este repositorio.

---

## 📜 Licencia

Proyecto desarrollado con fines académicos y de investigación.
