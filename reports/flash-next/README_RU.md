# Qwen3.8 Flash-Next UD-Q2_K_XL — 30 испытаний

24.11.2026. Один NVIDIA DGX Spark, 128 GB объединённой памяти (121 GiB видно ОС).

Strata с DFlash2 выигрывает все 12 прямых испытаний. Ollama 0.40.18 выигрывает 2 из 3 задач Hermes. Разница суммарного времени Hermes мала, а в Strata 4K наблюдалось пересечение запросов. Включены 57 исходных файлов Ollama с обезличиванием адреса контейнера; сверены все 15 измерений времени, хеши заданий, снимки памяти, метрики 12 прямых тестов и девять отметок PASS. Сравниваются рабочие конфигурации с различными механизмами ускорения.

Все девять функциональных проверок в каждой конфигурации отмечены PASS. Это не универсальная оценка качества. По одному прогону на задачу, статистическая значимость не установлена.


## Полное время (с)

| Case | ollama-0.40.18 | strata-dflash2 |
|---|---:|---:|
| hermes-4k | 67.162 | 85.504 |
| hermes-16k | 68.002 | 52.134 |
| hermes-short | 22.158 | 28.942 |
| dgx-4k | 26.237 | 8.789 |
| dgx-16k | 58.110 | 27.951 |
| dgx-32k | 88.330 | 31.662 |
| retrieval-r1 | 6.732 | 3.552 |
| retrieval-r2 | 6.213 | 3.682 |
| retrieval-r3 | 19.866 | 9.174 |
| tool-t1 | 3.203 | 1.343 |
| tool-t2 | 3.132 | 1.446 |
| tool-t3 | 3.321 | 2.134 |
| instructions-i1 | 2.492 | 1.125 |
| instructions-i2 | 2.894 | 1.481 |
| instructions-i3 | 3.233 | 1.537 |

## Суммарное время (с)

| Workload | ollama-0.40.18 | strata-dflash2 |
|---|---:|---:|
| Hermes | 157.323 | 166.579 |
| DGX | 172.677 | 68.402 |
| Retrieval | 32.811 | 16.408 |
| Tools | 9.656 | 4.922 |
| Instructions | 8.618 | 4.144 |
| Direct API | 223.763 | 93.876 |
| All | 381.086 | 260.455 |

## Генерация (ток/с)

| Case | ollama-0.40.18 | strata-dflash2 |
|---|---:|---:|
| hermes-4k | 30.520 | 49.977 |
| hermes-16k | 29.940 | 51.545 |
| hermes-short | 30.980 | 50.752 |
| dgx-4k | 26.924 | 61.500 |
| dgx-16k | 30.663 | 53.400 |
| dgx-32k | 30.045 | 51.900 |
| retrieval-r1 | 31.657 | 55.000 |
| retrieval-r2 | 31.718 | 54.600 |
| retrieval-r3 | 29.458 | 68.800 |
| tool-t1 | 29.282 | 80.500 |
| tool-t2 | 28.721 | 79.000 |
| tool-t3 | 29.416 | 77.700 |
| instructions-i1 | 29.499 | 77.000 |
| instructions-i2 | 29.728 | 69.900 |
| instructions-i3 | 30.978 | 71.700 |

## Обработка входа (новых ток/с)

| Case | ollama-0.40.18 | strata-dflash2 |
|---|---:|---:|
| hermes-4k | 877.550 | 1888.358 |
| hermes-16k | 872.620 | 1963.623 |
| hermes-short | 146.940 | 83.772 |
| dgx-4k | 890.024 | 1719.800 |
| dgx-16k | 945.315 | 2014.200 |
| dgx-32k | 892.106 | 2085.500 |
| retrieval-r1 | 960.354 | 1651.700 |
| retrieval-r2 | 962.245 | 1667.300 |
| retrieval-r3 | 947.523 | 2011.100 |
| tool-t1 | 480.612 | 527.900 |
| tool-t2 | 549.754 | 544.600 |
| tool-t3 | 562.027 | 556.300 |
| instructions-i1 | 230.509 | 194.700 |
| instructions-i2 | 196.325 | 208.100 |
| instructions-i3 | 180.656 | 192.000 |

For Flash-Next Hermes, Strata rate/token columns describe the first attributable model request, not the full multi-request task. For Qwen3.6 the first Hermes 4K rates are previously reported, not normalized source metrics.

Подробности и ограничения: [английский отчёт](README.md).
