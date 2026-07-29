---
title: "Control de Microclima Fúngico"
date: 2026-07-28
description: "Implementación de un sistema de control de temperatura y humedad en entornos cerrados."
tags: ["Sistemas Dinámicos", "Control", "Instrumentación"]
cover:
  image: "portada-ingenieria-01.jpg"
  alt: "Fotografía del entorno controlado"
math: true
---

## Exploración Inicial

Este proyecto aborda la regulación precisa de variables ambientales para el desarrollo fúngico. En esta primera etapa, nos centramos en la estabilización de la temperatura y la humedad relativa mediante instrumentación de bajo costo y algoritmos de control.

---

## Modelo Dinámico

# Modelo Dinámico V2

Para el diseño del controlador, partimos de una representación simplificada del sistema térmico:

$$ \dot{x}(t) = Ax(t) + Bu(t) + E w(t) $$

Donde $x(t)$ es el vector de estados, $u(t)$ la señal de control y $w(t)$ las perturbaciones exógenas.

---

## Visualización de Datos

A continuación, se presenta la captura de datos en tiempo real de la respuesta del sistema.

{{< grafico id="grafico01" >}}
// Todo lo que escribas aquí adentro se ejecuta como JavaScript puro
const tiempo = ['0 min', '5 min', '10 min', '15 min', '20 min'];
const temperatura = [18.0, 20.5, 22.8, 23.9, 24.1];

new Chart(ctx, {
    type: 'line',
    data: {
        labels: tiempo,
        datasets: [{
            label: 'Temperatura (°C)', 
            data: temperatura,
            borderColor: '#ff6b6b', 
            backgroundColor: 'rgba(255, 107, 107, 0.1)',
            fill: true
        }]
    },
    options: { responsive: true }
});
{{< /grafico >}}

---

## Visualización de Datos de la IMU en Tiempo Real

Para monitorizar el comportamiento físico y las vibraciones estructurales captadas por el sistema, el ESP32 envía tramas de la unidad inercial (9-DOF) hacia Firestore. 

El siguiente panel extrae esos datos directamente de la nube y grafica una ventana temporal estricta de 2 minutos (240 muestras por variable), referenciada a cero.

{{< telemetria_imu >}}

---