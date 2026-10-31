# hideseek-tables

Опубликованные таблицы баланса HideSeek. GitHub Pages отдаёт их игре:
`https://saiotix-games-co-ltd.github.io/hideseek-tables/<таблица>/<канал>.json`.

Руками файлы не править: публикует окно редактора Unity — оно проверяет набор целиком тем же правилом, что и игра, и делает один коммит на действие.

- `weapons/test.json`, `weapons/release.json` — каналы: каждый файл несёт полный набор, игра скачивает его одним запросом.
- `weapons/versions/<канал>/NNNN.json` — все опубликованные версии канала, не меняются; по ним откатываются.
- Release обновляется только продвижением выбранной версии Test.

## Как опубликовать таблицу оружия

1. Лист Google со столбцами `WeaponID | MagazineSize | ReserveAmmo` (другие столбцы не публикуются), доступ «все, у кого есть ссылка — просмотр». Его id и вкладка — в `Assets/_Project/Data/Balance/BalanceSettings.asset` (Publishing → Sheet Id, Sheet Gid).
2. Unity → `Saiotix/Таблицы/Оружие…` → «Загрузить лист Google» (или «CSV-файл…»). Окно покажет строки и примет набор только целиком: известные WeaponID без повторов, MagazineSize — целое больше нуля, ReserveAmmo — целое не меньше нуля.
3. «Загрузить каналы» → «Опубликовать новой версией в Test». Нужен доступ на запись в этот репозиторий (обычная учётка GitHub в git).
4. Окно ждёт, пока GitHub Pages начнёт отдавать новую версию (обычно 1–2 минуты, до 10 минут из-за кэша). Хост возьмёт её к следующему матчу, перезапуск игры не нужен; идущий матч доигрывается на своей версии.
5. Проверенную версию Test — кнопкой «В Release» в её строке. Откат — «Откатить сюда» у нужной версии канала.

Без окна: `Unity -batchmode -quit -projectPath <проект> -executeMethod Saiotix.HideSeek.EditorTools.TablesPublisherBatch.Run -tables-action publish-test -tables-csv <файл.csv>` (ещё `promote -tables-version N` и `rollback -tables-channel test|release -tables-version N`).

## 무기 테이블 게시 방법

1. Google 시트에 `WeaponID | MagazineSize | ReserveAmmo` 열을 둡니다(다른 열은 게시되지 않습니다). 공유는 "링크가 있는 모든 사용자 — 보기"로 설정합니다. 시트 id와 탭은 `Assets/_Project/Data/Balance/BalanceSettings.asset`(Publishing → Sheet Id, Sheet Gid)에 입력합니다.
2. Unity → `Saiotix/Таблицы/Оружие…` → "Загрузить лист Google"(또는 "CSV-файл…"). 창은 행을 보여 주고, 세트 전체가 맞을 때만 받아들입니다. 알려진 WeaponID는 중복 없이, MagazineSize는 0보다 큰 정수, ReserveAmmo는 0 이상의 정수여야 합니다.
3. "Загрузить каналы" → "Опубликовать новой версией в Test". 이 저장소에 쓰기 권한이 필요합니다(git의 일반 GitHub 계정).
4. 창은 GitHub Pages가 새 버전을 제공할 때까지 기다립니다(보통 1~2분, 캐시 때문에 최대 10분). 호스트는 다음 경기부터 새 버전을 사용하며 게임을 다시 시작할 필요는 없습니다. 진행 중인 경기는 기존 버전으로 끝까지 진행됩니다.
5. 검증된 Test 버전은 해당 행의 "В Release" 버튼으로 Release에 올립니다. 롤백은 원하는 버전의 "Откатить сюда"를 누릅니다.
