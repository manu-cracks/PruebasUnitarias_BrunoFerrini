# 🧪 Módulo de Aseguramiento de la Calidad de Software: Bruno Ferrini Checkout
## Laboratorio 05 (TDD) | Laboratorio 08 (CI) | Laboratorio 09 (SonarCloud)

![CI Jest](https://github.com/manu-cracks/PruebasUnitarias_BrunoFerrini/actions/workflows/ci-jest.yml/badge.svg)
[![Quality Gate](https://sonarcloud.io/api/project_badges/measure?project=manu-cracks_PruebasUnitarias_BrunoFerrini2&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=manu-cracks_PruebasUnitarias_BrunoFerrini2)
[![Coverage](https://sonarcloud.io/api/project_badges/measure?project=manu-cracks_PruebasUnitarias_BrunoFerrini2&metric=coverage)](https://sonarcloud.io/summary/new_code?id=manu-cracks_PruebasUnitarias_BrunoFerrini2)

---

## 📂 Documentos Académicos e Informes Completos
> 📌 **Acceso a Evidencias de Laboratorio:** Puedes visualizar, revisar y descargar todos los informes monográficos formales (PDF) que contienen las capturas de pantalla del proceso, logs detallados y análisis de métricas en el siguiente enlace:
>
> 📁 **[Carpeta de Google Drive - Informes de Laboratorio IS-489 (Manuel Ore)](https://docs.google.com/document/d/1WPDTy58ORqYQ6aLZ5MpLdj1MVMqgKcTaLO3Tx5ljZo0/edit?usp=sharing)**

---

## 📋 Información General

| Campo | Detalle |
|---------|---------|
| Facultad | Ingeniería de Minas, Geología y Civil |
| Escuela Profesional | Ingeniería de Sistemas |
| Asignatura | IS-489 Pruebas y Aseguramiento de Calidad de Software |
| Docente | Ing. Lizbeth Jaico Quispe[cite: 1, 2] |
| Semestre | 2026-I |
| Estudiante | Manuel Elias Yahve Ore Huasaja[cite: 2] |
| Sistema Analizado | Bruno Ferrini (E-commerce de moda y calzado)[cite: 2] |
| Módulo Evaluado | Procesamiento de Pago y Envío (Checkout) |
| Metodología | Test-Driven Development (TDD) + Integración Continua (CI) + Análisis Estático |

---

# 📖 Descripción del Sistema

**Bruno Ferrini** es una plataforma de comercio electrónico enfocada en la venta de calzado de cuero, ropa y accesorios de moda[cite: 2]. La solución de software automatiza los flujos de negocio esenciales para el cliente[cite: 2]:
- Visualización interactiva de productos.
- Gestión persistente del carrito de compras.
- Aplicación dinámica de cupones promocionales.
- Selección y cálculo de métodos de envío.
- Procesamiento de pagos transaccionales seguros con tarjetas bancarias.

---

# 🎯 Módulo Seleccionado: Checkout

Se seleccionó el módulo de **Checkout (Procesamiento de Pago y Envío)** por ser el núcleo crítico transaccional del sistema.

### Justificación Técnica
Cualquier fallo de lógica en esta sección compromete directamente:
- 💰 Las finanzas operativas de la organización.
- 🛒 La experiencia de usuario y tasa de conversión.
- 📦 La consistencia de datos en el inventario y logística.

La automatización de pruebas y el control estático garantizan la estabilidad del software ante refactorizaciones o actualizaciones continuas.

---

# ✅ Criterios de Aceptación (CAs)

* **CA-01:** Permitir la compra únicamente si existen productos en el carrito, la dirección y teléfono son válidos, y el número de tarjeta posee exactamente 16 dígitos numéricos.
* **CA-02:** Rechazar transacciones con montos netos inferiores a **S/. 50.00**.
* **CA-03:** Validar cupones de descuento bajo reglas de longitud (mínimo 5, máximo 10 caracteres) y verificar su existencia en la base de datos de la plataforma.
* **CA-04:** Validar que el formato del teléfono celular corresponda exactamente a 9 dígitos numéricos sin caracteres especiales.

---

# 🧪 Casos de Prueba Implementados

| ID | Caso de Prueba | Técnica Aplicada | Estado |
|------|------|------|------|
| TC-01 | Compra exitosa estándar | Clase Válida | ✅ PASS |
| TC-02 | Cupón con longitud mínima válida | Clase Válida | ✅ PASS |
| TC-03 | Dirección vacía | Edge Case | ✅ PASS |
| TC-04 | Teléfono con caracteres especiales | Edge Case | ✅ PASS |
| TC-05 | Carrito vacío | Clase Inválida | ✅ PASS |
| TC-06 | Tarjeta incompleta | Clase Inválida | ✅ PASS |
| TC-07 | Monto menor a S/.50 | Clase Inválida | ✅ PASS |
| TC-08 | Cupón inexistente | Clase Inválida | ✅ PASS |
| TC-09 | Cupón menor a 5 caracteres | Valores Límite | ✅ PASS |
| TC-10 | Cupón mayor a 10 caracteres | Valores Límite | ✅ PASS |

---

# 🔄 Flujo del Pipeline de Aseguramiento de la Calidad (QA)

El proyecto implementa un ecosistema moderno de desarrollo enfocado en la estabilidad del código a través de tres fases complementarias:

### 1️⃣ Fase TDD (Laboratorio 05)
El desarrollo se guio bajo la metodología **Test-Driven Development**:
* **Fase RED:** Escritura de la suite de pruebas unitarias en **Jest** definiendo las reglas de los CAs. Las pruebas fallaron exitosamente debido a la inexistencia de lógica funcional.
* **Fase GREEN:** Codificación de la lógica mínima requerida en `checkoutBrunoFerrini.js` hasta lograr que la totalidad de los casos de prueba se ejecuten con éxito (100% de éxito).

### 2️⃣ Fase de Integración Continua - CI (Laboratorio 08)
Se automatizó la ejecución de la suite de pruebas mediante un workflow nativo de **GitHub Actions** (`ci-jest.yml`). 
* El pipeline se activa ante cada evento de `push` o `pull_request` sobre la rama `main`.
* Levanta un contenedor con Ubuntu, inicializa Node.js, instala dependencias, ejecuta las pruebas de Jest y exporta dinámicamente un reporte físico de cobertura (`coverage/lcov.info`) como un **Artefacto de compilación**.

### 3️⃣ Fase de Análisis Estático de Código (Laboratorio 09)
Se integró el pipeline de GitHub Actions con **SonarCloud** para auditar la salud general de la aplicación sin interferir con el flujo mecánico de ejecución:
* **Quality Gate:** Aprobado (**PASSED**) de forma automática al superar el umbral mínimo del 70% de cobertura.
* **Análisis de Deuda Técnica:** 0 minutos de deuda técnica acumulada y 0 Code Smells detectados.
* **Seguridad y Confiabilidad:** Clasificación A (0 Vulnerabilidades, 0 Bugs y 0.0% de código duplicado).

---

# 📂 Estructura del Proyecto

```text
bruno-ferrini-checkout-tdd/
│
├── .github/
│   └── workflows/
│       └── ci-jest.yml             # Pipeline de Integración Continua (Actions)
│
├── src/
│   └── checkout/
│       └── checkoutBrunoFerrini.js # Lógica de negocio del Checkout
│
├── tests/
│   └── checkoutBrunoFerrini.test.js # Suite de pruebas unitarias (Jest)
│
├── coverage/                       # Reportes locales de cobertura (omitidos en Git)
│
├── sonar-project.properties        # Configuración del escáner de SonarCloud
├── package.json                    # Dependencias y scripts del proyecto
└── README.md                       # Documentación principal del repositorio