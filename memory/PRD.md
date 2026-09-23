# PRD — App de gramática para niños (5 sentidos)

## Problema original
App educativa de gramática EN/ES/Mixto. El usuario pidió convertirla en la
**versión para niños** centrada en los 5 sentidos humanos.

## Decisiones del usuario
- Reemplazar la app por la versión para niños (se quitan M2.A, M2.B, M3.A, M4.A del home).
- Home muestra solo: M1.A, M1.B, Tita I, Tita II.
- M1.A y M1.B usan SOLO los 5 sentidos (see, touch, smell, taste, hear) con ícono.
- Sentidos también en español (ver, tocar, oler, saborear, oír) para modo ES/Mixto.
- Tita I y Tita II se dejan igual.

## Arquitectura
- Frontend: Expo Router (React Native). Backend: FastAPI + MongoDB.
- TTS vía `/api/tts` (OpenAI TTS con EMERGENT_LLM_KEY) reproducido con expo-audio.

## Implementado (2026-09-23)
- Home (`app/index.tsx`): array MODULES reducido a 4 tarjetas; íconos eye/flower.
- Contenido de sentidos (`src/data/modules.ts`): SENSES_EN / SENSES_ES + SENSE_ICONS,
  M1.A y M1.B ahora usan los 5 sentidos; default "see"/"ver".
- Selector de verbos (`src/components/PracticeScreen.tsx`): soporta `verbIcons`,
  muestra chips grandes de 2 columnas con ícono, oculta el buscador para los sentidos.
- Modo mixto (`src/data/bilingual.ts`): añadidas equivalencias taste↔saborear,
  hear↔oír, tocar/oler/saborear/oír → touch/smell/taste/hear.
- Títulos (`src/i18n.ts`): M1.A "Los 5 sentidos / The 5 senses", M1.B "Sentidos continuos".
- Restaurados `.env` de backend y frontend (se habían perdido al recargar entorno).

## Verificado
- M1.A EN: "I can see." / "I cannot see." / "Can I see?"
- M1.B EN: "I can be seeing." (continuo)
- ES: "Yo puedo ver." con sentidos en español.
- Home con 4 módulos y selector de 5 sentidos con íconos.

## Backlog / próximos
- P1: pronunciación automática al generar; imágenes/ilustración por sentido.
- P2: modo juego/quiz de sentidos; recompensas para niños.
