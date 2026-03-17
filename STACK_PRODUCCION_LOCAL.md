# Stack de producción 100% local (coste 0 en suscripciones)

Este stack está pensado para ejecutar **todo en local/on-prem** sin depender de servicios SaaS de pago.

## 1) Entrenamiento e inferencia
- **Python 3.11+**
- **PyTorch** (CPU/GPU local)
- **OpenCV** (preprocesado de imagen)
- **Ultralytics YOLOv8** o **RT-DETR** (detección)
- **U-Net** o **SegFormer** (segmentación)
- **TrOCR** o **PaddleOCR** (OCR)

## 2) Servicio de producción
- **FastAPI + Uvicorn** para exponer API REST
- **Docker + Docker Compose** para empaquetado reproducible
- **Nginx** como reverse proxy local
- **PostgreSQL** para persistencia de metadatos
- **MinIO** para almacenamiento local tipo S3 (imágenes, resultados)
- **Redis** para cola/cache (opcional)

## 3) Orquestación de procesos
- **Celery** (con Redis) para tareas pesadas asincrónicas
  - Pipeline recomendado:
    1. Ingesta imagen
    2. Preprocesado OpenCV
    3. Detección + segmentación
    4. OCR
    5. Reconstrucción estructural (JSON final)

## 4) Etiquetado de datos (sin suscripción)
- **CVAT self-hosted** (Docker)
- **Label Studio Community Edition** (self-hosted)

## 5) Experimentos y monitoreo (sin SaaS)
- **MLflow local** (tracking server en Docker)
- **Weights & Biases solo si self-hosted**; para coste 0 estricto, prioriza MLflow
- **Prometheus + Grafana** para métricas del servicio
- **Loki + Promtail** para logs centralizados locales

## 6) Configuración mínima de infraestructura local
- 1 servidor con GPU (ideal) o CPU robusta
- Linux + Docker Engine
- Estructura sugerida:
  - `api`: FastAPI
  - `worker`: Celery + modelos
  - `db`: PostgreSQL
  - `object_store`: MinIO
  - `queue`: Redis
  - `monitoring`: Prometheus/Grafana/Loki

## 7) Coste 0 real: decisiones clave
1. Evitar APIs externas de OCR/visión.
2. Evitar plataformas SaaS de MLOps.
3. Usar solo componentes OSS desplegados localmente.
4. Versionar modelos en disco/NAS o en MinIO.
5. Automatizar backup local (scripts + cron).

## 8) Stack final recomendado (producción local)
- **Modelado:** PyTorch + YOLOv8/RT-DETR + U-Net/SegFormer + TrOCR/PaddleOCR
- **Backend:** FastAPI + Celery + Redis
- **Datos:** PostgreSQL + MinIO
- **Infra:** Docker Compose + Nginx
- **MLOps:** MLflow local
- **Observabilidad:** Prometheus + Grafana + Loki
- **Anotación:** CVAT/Label Studio self-hosted

## 9) Riesgos y mitigación
- **Latencia alta en CPU:** usar colas async y lotes; migrar inferencia crítica a GPU local.
- **Drift por estilos de dibujo:** ciclo de reetiquetado mensual + fine-tuning continuo.
- **Errores OCR en manuscrito:** diccionario técnico + normalización + modelo afinado con datos propios.

## 10) Roadmap rápido
- **Semana 1-2:** levantar infraestructura local (Docker Compose), API base y pipeline mínimo.
- **Semana 3-4:** entrenamiento inicial detección/segmentación/OCR con dataset base.
- **Semana 5-6:** observabilidad, hardening, pruebas de carga y despliegue estable.
