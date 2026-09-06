# janosrf-web-flasher

Webowy flasher firmware JanosRF na **ESP32-C5** (GitHub Pages + Web Serial / esptool-js).

## Strona

https://elpadrino26.github.io/janosrf-web-flasher/

Wymaga **Chrome** lub **Edge** (Web Serial API).

## Jak flashować

1. Podłącz ESP32-C5 USB-UART.
2. Otwórz stronę powyżej.
3. Kliknij **Połącz** i wybierz port szeregowy.
4. Kliknij **Flashuj** — domyślnie używane są biny z `latest/`.
5. Opcjonalnie nadpisz poszczególne pliki lokalnymi `.bin`.

## Mapa flasha

| Offset   | Plik                   | Źródło domyślne              |
|----------|------------------------|------------------------------|
| `0x2000` | `bootloader.bin`       | `latest/bootloader.bin`      |
| `0x10000`| `partition-table.bin`  | `latest/partition-table.bin` |
| `0x20000`| `projectZero.bin`      | `latest/projectZero.bin`     |

Parametry (jak w CLI):

```bash
esptool --chip esp32c5 \
  -b 460800 \
  --before=default-reset \
  --after=hard-reset \
  write-flash \
  --flash-mode dio \
  --flash-freq 80m \
  --flash-size 8MB \
  0x2000 bootloader.bin \
  0x10000 partition-table.bin \
  0x20000 projectZero.bin
```

## Aktualizacja firmware

Wgraj nowe pliki do katalogu `latest/` (te same nazwy) i wypchnij na `main`. Strona Pages od razu serwuje nowe biny.
