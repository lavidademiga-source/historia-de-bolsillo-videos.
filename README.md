# Historia de Bolsillo · vídeos para publicar

Buzón diario de Shorts del canal **Historia de Bolsillo**. Cada mañana se añade una carpeta con los dos vídeos de un día y su `manifest.json`. La web de publicación lee el manifiesto y programa cada vídeo en YouTube.

## Estructura

```
AAAA-MM-DD/
  AAAA-MM-DD_1_tema.mp4   # pase de las 18:30 (hora de Madrid)
  AAAA-MM-DD_2_tema.mp4   # pase de las 21:30 (hora de Madrid)
  manifest.json
```

Normalmente la carpeta nueva corresponde a la fecha de dentro de 7 días.

## manifest.json

```json
{
  "canal": "Historia de Bolsillo",
  "fecha": "AAAA-MM-DD",
  "palabra_clave": "DINERO",
  "videos": [
    {
      "orden": 1,
      "archivo": "AAAA-MM-DD_1_tema.mp4",
      "url_descarga": "https://raw.githubusercontent.com/lavidademiga-source/historia-de-bolsillo-videos./main/AAAA-MM-DD/AAAA-MM-DD_1_tema.mp4",
      "publicar_en": "AAAA-MM-DDT18:30:00+01:00",
      "zona_horaria": "Europe/Madrid",
      "titulo": "máximo 60 caracteres",
      "descripcion": "texto + fuentes + hashtags, lista para pegar",
      "hashtags": ["#Shorts", "..."],
      "etiquetas": ["historia", "..."],
      "categoria_id": "27",
      "idioma": "es",
      "para_ninos": false,
      "contenido_sintetico_realista": false,
      "privacidad_hasta_publicar": "private",
      "comentario_fijado": "pregunta para fijar como primer comentario",
      "duracion_s": 34
    }
  ]
}
```

Correspondencia con la YouTube Data API (`videos.insert`):

| Campo del manifiesto | YouTube API |
| --- | --- |
| `titulo` | `snippet.title` |
| `descripcion` | `snippet.description` |
| `etiquetas` | `snippet.tags` |
| `categoria_id` | `snippet.categoryId` (27 = Educación) |
| `idioma` | `snippet.defaultLanguage` y `snippet.defaultAudioLanguage` |
| `privacidad_hasta_publicar` + `publicar_en` | `status.privacyStatus = "private"` + `status.publishAt` (para programar) |
| `para_ninos` | `status.selfDeclaredMadeForKids` |
| `contenido_sintetico_realista` | `status.containsSyntheticMedia` (animación no realista: `false`) |
| `comentario_fijado` | publicar con `commentThreads.insert` después de que el vídeo sea público; fijarlo se hace a mano en YouTube Studio |

`publicar_en` lleva el desfase de Madrid de esa fecha (+01:00 en invierno, +02:00 en verano).

Los vídeos son MP4 H.264 vertical 1080×1920, 30 fps, AAC, de 34 a 50 s y menos de 20 MB.
