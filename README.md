# Blueprint: Detección Inteligente y Registro con Gemini y Telegram para Home Assistant

## Descripción

Este blueprint permite monitorizar múltiples cámaras con sensores de movimiento para detectar actividad, analizar imágenes con Gemini Pro Vision (llmvision) y enviar notificaciones vía Telegram con botones interactivos para gestionar alertas. Además, registra automáticamente eventos importantes en un historial dentro de Home Assistant.

---

## Características

- Soporta múltiples cámaras y sensores de movimiento configurables.
- Evita notificaciones repetidas con un tiempo de espera configurable.
- Condición activa solo cuando la alarma está en modo `armed_away`.
- Notificaciones Telegram con botones para "Ignorar" o "Marcar como importante".
- Historial de eventos guardado en un `input_text` dentro de Home Assistant.
- Configurable para notificaciones de texto o TTS.

---

## Requisitos previos

- Home Assistant actualizado (versión 2024+ recomendada).
- Servicio llmvision con Gemini Pro Vision funcionando.
- Bot de Telegram configurado para enviar notificaciones y manejar botones inline.
- Panel de alarma integrado en Home Assistant.
- Entidad `input_text` creada para el registro de eventos.

---

## Variables del Blueprint

| Variable             | Descripción                                      | Tipo         | Ejemplo / Valor por defecto                        |
|----------------------|------------------------------------------------|--------------|---------------------------------------------------|
| `cameras`            | Lista de cámaras a monitorizar                   | Entidad lista| `camera.camara_1_exterior_calidad_fluent`, etc.   |
| `motion_sensors`     | Lista de sensores binarios de movimiento         | Entidad lista| `binary_sensor.camara_1_exterior_movimiento`, etc.|
| `input_text_entity`  | Entidad para registrar eventos                    | Entidad      | `input_text.eventos_camaras`                       |
| `telegram_chat_id`   | ID del chat o usuario para Telegram               | Texto        | `-123456789`                                       |
| `alarm_panel_entity` | Entidad panel de alarma para condición armado away| Entidad      | `alarm_control_panel.mi_panel`                     |
| `delay_notification` | Tiempo mínimo entre notificaciones (segundos)    | Número       | `60`                                               |
| `tts_notification`   | Activar notificación TTS                           | Booleano     | `false`                                            |

---

## Instalación

1. Copia el archivo YAML del blueprint en `config/blueprints/automation/`.
2. En Home Assistant, ve a **Configuración > Automatizaciones > Blueprints** y haz clic en **Importar Blueprint** para cargarlo.
3. Crea una automatización basada en este blueprint y configura tus cámaras, sensores, Telegram, etc.
4. Asegúrate de crear el siguiente `input_text` en tu configuración si no lo tienes:

```yaml
input_text:
  eventos_camaras:
    name: Registro de eventos cámaras
    initial: ""
    max: 1000
