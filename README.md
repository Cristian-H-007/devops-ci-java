# DevOps CI con GitHub Actions, JaCoCo y SonarCloud

Proyecto Java + Maven de ejemplo (calculadora de descuentos) usado para el reto práctico de **Calidad de Software – UNAC**.
Cada `push` o `pull request` hacia `main` ejecuta automáticamente un pipeline de integración continua.

## ¿Qué hace el pipeline? (`.github/workflows/ci.yml`)

1. **Checkout** del repositorio (con historial completo para SonarCloud).
2. **Java 25** (Temurin) con caché de dependencias Maven.
3. **`mvn clean verify`**: compila, ejecuta las pruebas unitarias (JUnit), genera el reporte de cobertura con **JaCoCo** y valida que cada clase tenga **mínimo 95 % de cobertura de líneas**. Si una prueba falla o la cobertura baja, el pipeline falla.
4. **SonarCloud Scan**: envía el código y el reporte `jacoco.xml` a SonarCloud para el análisis de calidad (bugs, code smells, cobertura, duplicación y Quality Gate).

## Estructura

```
.github/workflows/ci.yml          → workflow de GitHub Actions
pom.xml                           → dependencias, Surefire y JaCoCo (report + check 95 %)
sonar-project.properties          → configuración de SonarCloud
src/main/java/.../DiscountCalculator.java
src/main/java/.../InvalidPurchaseException.java
src/test/java/.../DiscountCalculatorTest.java
```

## Reglas de negocio probadas

| Cliente | Monto | Descuento |
|---|---|---|
| Premium | ≥ 500 | 20 % |
| Premium | < 500 | 10 % |
| Regular | ≥ 500 | 5 % |
| Regular | < 500 | 0 % |
| Cualquiera | ≤ 0 | `InvalidPurchaseException` |

## Ejecutar localmente

```bash
mvn clean verify
# Reporte de cobertura: target/site/jacoco/index.html
```

## Evidencias

- Ejecuciones del pipeline: pestaña **Actions** de este repositorio.
- Checks en Pull Requests: pestaña **Pull requests**.
- Análisis de SonarCloud: https://sonarcloud.io (proyecto vinculado a este repositorio).
- Video de demostración: _(enlace de YouTube)_

## Integrantes

- Cristian — _(completar)_
