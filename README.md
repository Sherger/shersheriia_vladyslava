# Vladyslava Shersheriia — CV & Portfolio

Сайт-резюме с портфолио. Статичный (HTML + CSS + JS, без сборки), для GitHub Pages. Языки EN / UA (переключатель в шапке, ссылка `?lang=uk` открывает украинскую версию).

## Структура

```
index.html            разметка и английские тексты
i18n.js               украинские переводы (ключи = data-i18n в index.html)
styles.css            дизайн; палитра в начале файла (--accent, --band …)
script.js             язык, портфолио, полноэкранный просмотр, копирование контактов
data/works.json       список работ (EN + UA); порядок в файле = порядок на сайте
assets/works/web/     сжатые видео, обложки и статики, которые показывает сайт
Creo_*, Фото-*        оригиналы (в git не попадают, см. .gitignore)
assets/photo.jpg      аватар (квадрат 800×800, на сайте круглый)
assets/og-image.jpg   превью ссылки для Telegram/LinkedIn
assets/Vladyslava_Shersheriia_CV_2026_EN.pdf   резюме для скачивания
```

## Добавить работу

```bash
ffmpeg -i Creo_12.mp4 -c:v libx264 -preset slow -crf 23 -maxrate 5M -bufsize 10M -pix_fmt yuv420p -vf "scale='min(1080,iw)':-2" -r 30 -c:a aac -b:a 128k -movflags +faststart assets/works/web/creo-12.mp4
ffmpeg -ss 0.6 -i assets/works/web/creo-12.mp4 -frames:v 1 -vf "scale=720:-2" -q:v 4 assets/works/web/creo-12.jpg
```

Затем запись в `data/works.json`. Необязательные поля: `"badge"` (плашка, например «100% AI-generated»), `"type": "image"` для статики, `"format": "landscape"` для горизонтальных работ (две горизонтальные встают в один ряд).

## Локально

```bash
npx http-server . -p 5174 -c-1
```

Открыть http://localhost:5174

## Деплой на GitHub Pages

1. Создать **публичный** репозиторий, в этой папке: `git init`, `git add .`, `git commit -m "CV and portfolio site"`, `git branch -M main`, `git remote add origin https://github.com/USERNAME/REPO.git`, `git push -u origin main`.
2. **Settings → Pages → Deploy from a branch**, `main` / `(root)`.
3. Сайт: https://sherger.github.io/shersheriia_vladyslava/ (og:image и og:url в index.html уже указывают на этот адрес).

После правок `styles.css`, `script.js` или `i18n.js` увеличивай `?v=1` в их подключении в `index.html`, чтобы браузеры не показывали старую версию.
