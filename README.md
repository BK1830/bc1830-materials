# Публичные материалы БК1830

Шесть ранее опубликованных HTML: `/`, `/pd/`, `/remarked/`, `/remarked/guest-journey.html`, `/remarked/part-1.html`, `/remarked/part-2.html`.

Публичный адрес после переноса: https://docs.bc1830hb.com/

## Как обновлять

`main` — рабочие черновики. GitHub Pages публикует только корень ветки `gh-pages`. Обычный коммит в `main` сайт не меняет. Пользовательское решение «публикуй» нужно перед каждым новым выпуском.

1. Создать рабочую ветку от `main`, изменить только нужные материалы; не добавлять секреты и закрытые документы в этот public repo.
2. Показать Олегу diff и локальный preview. В корне checkout: `python3 -m http.server 8000 --bind 127.0.0.1`, затем http://127.0.0.1:8000/. Проверить пути с корня сайта. Отдельные публичные PR preview не настроены.
3. После приёмки сохранить подготовленный commit в `main`. После явного «публикуй» обновить production ветку: `git switch gh-pages`, `git merge --ff-only main`, `git push origin gh-pages`. Если fast-forward невозможен, остановиться и проверить расхождение без force push.
4. Дождаться Pages deployment и проверить все шесть production URL: HTTP 200, действующий TLS, ожидаемые SHA256 тел ответов. Записать commit/deployment и результат.

Рабочий checkout: `/Users/oleg/Developer/Claude/bc1830-materials`. Первоначальный неизменённый bundle и manifest сохранены локально: `/Users/oleg/Downloads/bc1830-static-materials-2026-11-16/`.

## Настройки публикации

GitHub Settings → Pages → Deploy from a branch → `gh-pages` → `/ (root)`. CI не добавлен; GitHub выполняет штатный Pages branch deployment.
Custom domain: `docs.bc1830hb.com`. DNS: только CNAME `docs` → `bk1830.github.io`, TTL 300, DNS only. Имя репозитория в DNS target не добавлять. `hb.bc1830hb.com` и `demo.bc1830.ru` не относятся к этому сайту.

## Если сайт сломался

Найти последний проверенный production commit в истории `gh-pages`. Сделать обычный revert ошибочного выпуска в production ветке, проверить diff, получить разрешение на откат и push без переписывания истории. Согласовать затем `main` с фактической production версией.
При проблеме сертификата сначала проверить Pages → custom domain / certificate и DNS; не отключать TLS verification. HTTPS enforce включается после готовности сертификата.

До миграции DNS был `docs A 166.88.182.53`, TTL 300, DNS only. Возврат этой записи не гарантирует восстановление старого origin: его доступность надо проверить отдельно. Не менять соседний `hb` Access/Tunnel.

## Первая миграция

Задача: https://github.com/BK1830/bc1830-materials/issues/1 . При первом выпуске default Pages URL проверяется до настройки custom domain и DNS. Проектный URL содержит `/bc1830-materials/`; корневые ссылки HTML рассчитаны на окончательный custom domain. HTML байты ради временного адреса не меняются.
