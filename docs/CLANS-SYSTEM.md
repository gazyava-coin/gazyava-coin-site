# Gazyava Tap — система кланов

## Основные правила
- Один игрок может состоять только в одном клане.
- Создать клан можно с названием длиной 3–24 символа; название уникально без учёта регистра.
- В клане максимум 25 участников.
- Вступление — по 8-символьному коду приглашения.
- У создателя роль лидера. Если лидер выходит, руководство автоматически переходит участнику, который вступил раньше остальных. Если лидер был последним, клан расформировывается.

## Командный прогресс
- Каждый подтверждённый сервером тап увеличивает недельный вклад игрока и клана.
- Недельный период начинается в понедельник 00:00 UTC.
- Личный вклад участника и общий вклад клана отображаются отдельно.
- В рейтинге показываются 10 лучших кланов по недельным тапам; при равенстве учитываются накопленные тап-очки и дата создания.

## Недельные задания
| Этап | Тапы клана за неделю | Награда каждому участнику |
|---|---:|---:|
| Облачная команда | 5 000 | +25 игровых очков |
| Командный шторм | 15 000 | +75 игровых очков |
| Легендарный рывок | 30 000 | +150 игровых очков |

Один участник может забрать награду за достигнутый этап, после чего она начисляется всем участникам клана на момент получения. Каждый этап можно получить один раз за неделю.

## Безопасность и сервер
- Прогресс тапов учитывается в `tap_player` на сервере.
- Создание, вступление, выход, рейтинг и выдача наград выполняются RPC через Edge Function `game`.
- Telegram initData проверяется до вызова RPC.
- Таблицы `clans`, `clan_members` и `clan_weekly_claims` защищены RLS; прямые права `anon` и `authenticated` отозваны.
- Награды начисляются транзакционно, повторные выплаты блокируются первичным ключом недельной награды.

Клановые очки — внутриигровой счёт Gazyava Tap, не токен и не денежное обязательство.


## Чат, заместители и Telegram-приглашения

- Внутри клана доступен общий чат с последними 50 сообщениями.
- Сообщение ограничено 300 символами; серверный лимит отправки — одно сообщение раз в 3 секунды на игрока.
- Сообщения читаются и отправляются только через проверенную Edge Function и RPC. Прямые права на таблицу `clan_messages` закрыты.
- Лидер может назначать участников заместителями, снимать роль заместителя и исключать участников.
- Заместитель может исключать обычных участников, но не лидера и не других заместителей.
- Telegram-ссылка приглашения включает код клана в параметре `startapp=clan_<код>`; при открытии игры поле вступления заполняется автоматически.
- Параметр `clan_` исключён из обработки реферальных кодов, чтобы клановые приглашения не запускали реферальную логику.
- Чат обновляется при открытой вкладке клана с интервалом 15 секунд; также доступно ручное обновление.


## Клановые войны (24-часовые матчи)

- Лидер клана с минимум тремя участниками может поставить клан в очередь поиска.
- Матчмейкинг подбирает первый доступный клан-соперник из очереди; один клан не может одновременно участвовать в нескольких активных битвах.
- После нахождения соперника начинается 24-часовая битва. Каждый подтверждённый сервером тап участника добавляет 1 боевое очко его клану; очки учитываются триггером от изменения серверного дневного прогресса, а не из клиентского запроса.
- Итог определяется сравнением боевых очков: победа — +200 игровых очков каждому участнику на момент создания матча, ничья — +100, поражение — +50.
- Состав награждаемых фиксируется при старте матча. Каждый участник может получить награду только один раз; раннее получение и повторная выплата блокируются на сервере.
- Очередь, матчи и список участников защищены RLS; прямые права anon и authenticated закрыты. Вызовы идут через Edge Function game после проверки Telegram initData.
- Вклад в войну считается только по тапам, принятым сервером, поэтому клиент не может подделать боевой счёт.
- Клановые войны используют внутриигровые очки Gazyava Tap и не являются денежной или токеновой наградой.

## Клановые сезоны и дивизионы

- Сезон длится 7 дней и начинается в понедельник 00:00 UTC.
- Каждый серверно подтверждённый тап записывается в сезонный счёт клана и личный вклад участника.
- Дивизионы определяются сезонным результатом: Бронза — до 9 999 тапов; Серебро — 10 000–49 999; Золото — 50 000–149 999; Алмаз — от 150 000. Текущая карточка показывает дивизион и изменение относительно прошлого сезона.
- Вклад и место клана доступны в сезонном рейтинге. Награды предыдущего сезона можно получить после смены недели, если игрок сделал хотя бы один тап в прошлом сезоне.
- Награда каждому участнику, который сделал вклад: 1-е место +500, 2-е +300, 3-е +200, места 4–10 +100, остальные участвовавшие кланы +25 игровых очков.
- Топ-10 получает сезонный трофей соответствующего ранга. Участники клана-чемпиона дополнительно получают постоянный скин «Чемпион сезона».
- Сезонные начисления защищены уникальным ключом на игрока и сезон; повторная выплата блокируется.
- Сезонные таблицы закрыты RLS, прямые права anon/authenticated отсутствуют; действия проходят через Edge Function game после проверки Telegram initData.

## Карта мира Gazyava

Вкладка «Мир» добавляет интерактивную карту из шести регионов:
- Облачная деревня — доступна сразу.
- Мятный лес — 1 000 игровых очков.
- Огненные горы — 5 000.
- Ледяные земли — 10 000.
- Космическая долина — 15 000.
- Золотое королевство — 50 000.

Карта показывает текущий уровень исследователя, прогресс до следующего региона и описание выбранной земли. Открытие региона зависит от текущего серверного игрового счёта; отметка «исследовано» хранится локально на устройстве и не является игровой наградой. Карта не начисляет очки и не меняет серверный баланс.


### Атлас и журнал экспедиций

Карта дополнена атласом выбранного региона:
- Показывается главная достопримечательность открытого региона; для закрытых земель она скрыта.
- Отдельная шкала показывает путь к ближайшему следующему региону и оставшееся количество очков.
- При выборе доступной земли она отмечается исследованной и добавляется в журнал путешествий.
- Журнал показывает посещённые регионы в порядке последнего посещения; повторный визит поднимает регион в начало списка.
- Список посещений и отметки исследования сохраняются в localStorage текущего устройства. Они не синхронизируются между устройствами, не дают игровых очков и не являются серверно подтверждёнными достижениями.


### Тайные места и точки интереса карты

- В каждом из шести регионов добавлены три точки интереса с собственными названиями, символами и описаниями.
- Первые две точки доступны после открытия региона. Третья — секретная: она становится доступной после нахождения первых двух.
- Найденные точки отмечаются в карточке региона; счётчик показывает прогресс исследования (0–3).
- Найденные места сохраняются в localStorage устройства. Это локальные открытия без игровых очков, серверных наград или влияния на баланс.
- Проверка открытия региона выполняется по текущему игровому счёту на клиенте; это исследовательская/косметическая механика, а не защищённая серверная награда.


## World treasures and relic collection (November 2026)

The world map now includes six regional treasure chests. A chest becomes available only after the region is unlocked by the player's displayed score and all three local points of interest in that region have been discovered. Opening it grants one cosmetic relic:

- Cloud Village — Cloud Compass (common)
- Mint Forest — Mint Crystal (uncommon)
- Fire Mountains — Spark Heart (rare)
- Frost Lands — Frost Rune (rare)
- Cosmic Valley — Star Lens (epic)
- Golden Kingdom — Royal Seal (legendary)

Collecting all six relics unlocks the local-only Secret Chest and the Heart of Gazyava discovery. Four exploration titles track milestones: Scout (3 points of interest), Cartographer (3 regions), Collector (3 relics), and Gazyava Legend (secret chest opened).

Storage keys: `gazyava_world_chests`, `gazyava_world_artifacts`, and `gazyava_world_secret`. These collectibles, titles, and world discovery remain in browser localStorage and are cosmetic only. They do not award game points, affect player balances, or provide server-authoritative ownership. Clearing browser storage or switching devices resets this local collection. Do not use it as eligibility for token distributions or competitive rewards without moving validation to trusted server-side state.


## Weekly clan boss raid (November 2026)

Each clan has one shared weekly boss, with a fresh 100,000 HP pool from Monday 00:00 UTC. Boss appearance rotates through Cloud Titan, Frost Golem, Spark Dragon, and Star Guardian. Every server-confirmed tap recorded in `daily_progress` deals 1 damage while the boss is alive. Damage is tracked per player and per clan-week; taps after defeat do not increase contribution.

The Friends tab shows boss HP, phase thresholds (70%, 40%, 10%), personal damage/rank, and the top 10 contributors. A player who contributed at least 1 damage can claim once after defeat. Server rewards: rank 1 +500 points, rank 2 +300, rank 3 +200, all other contributors +100. Claiming is atomic and guarded by a unique key. The Edge Function `game` v38 exposes `clan_boss_status` and `claim_clan_boss_reward`; JWT verification remains enabled. Boss state, damage, and claims are RLS-enabled and inaccessible to anon/authenticated roles; only the service role is granted direct table/function access.

Tables: `clan_bosses`, `clan_boss_damage`, `clan_boss_claims`. Boss damage is driven by a trigger on server-maintained `daily_progress`, not by client-submitted damage. SQL integration test covered initial and incremental damage, lethal hit, no post-defeat damage, status, reward balance, and claim. Browser JavaScript syntax was checked; Telegram live gameplay was not tested.


## Player XP and levels (November 2026)

The play screen now displays a server-derived lifetime XP bar. XP equals lifetime server-confirmed taps from `player_achievement_stats.lifetime_taps`; it is not spendable score. Levels and titles: 1 Novice (0), 2 Apprentice (100), 3 Tapper (500), 4 Explorer (1,500), 5 Master (5,000), 6 Expert (10,000), 7 Hero (25,000), 8 Legend (50,000), 9 Myth (100,000). The progression RPC `get_player_progression(bigint)` returns current/next level and progress percentage. Edge Function `game` v39 exposes `player_progression`, with Telegram initData validation and service-role-only RPC execution. Integration checks covered level 1, level 2, level 8 and max level 9.
