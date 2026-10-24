# YouTube jako zdroj

Větev pro téma, kde záleží na tom, co se říká ve videích (nástroj, trend, osobnost).

1. **Discovery**: hledání `<téma> site:youtube.com` a `yt-dlp --flat-playlist --print "%(title)s | %(view_count)s | %(upload_date)s | %(webpage_url)s" "ytsearchdate10:<téma>"`; u konkrétního kanálu `"<URL kanálu>/videos"`. Vyber 5 videí podle relevance, data a sledovanosti.
2. **Přepis**, video po videu, ne paralelně (YouTube vrací 429 při dávce): `python3 ~/.agents/skills/research-lib/scripts/youtube_transcript.py "URL"`. Skript zkusí yt-dlp titulky a pak `youtube-transcript-api`; když nic, video přeskoč a do reportu napiš proč.
3. **Extrakce** z každého přepisu: 3 až 5 klíčových bodů, max 3 doslovné citace, jeden unikátní insight, vše s `[video: URL]`. Co v přepisu není, do reportu nejde.
4. **Cross-video analýza**: shoda, rozdíly, trend. Do formátu reportu v [SKILL.md](SKILL.md) přidej sekce „Videa“ (název, URL, views, datum, body, citace) a „Cross-video analýza“.

Hotovo, když má každé video přepis nebo poznámku, proč ne, a každý fakt v syntéze nese odkaz na video.
