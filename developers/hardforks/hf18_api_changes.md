# HF18: Изменения в API

В версии HF•18 реализованы новые функциональные и технические возможности, предоставляющие пользователям более удобное взаимодействие с системой, повышенную защиту от злоупотребления голосованием, а также повышающие быстродействие системы за счет более оптимального перераспределения методов между плагинами API.

* [Новые функциональные возможности в HF•18](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#перечень-новых-функциональных-возможностей-в-hf18)
* [Новые технические возможности в HF•18](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#перечень-новых-технических-возможностей-в-hf18)
* [Измененные и новые плагины API в HF•18](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#измененные-и-новые-плагины-в-hf18):
  * [private\_message](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#изменения-в-плагине-privatemessage)
  * [witness\_api](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новый-плагин-witnessapi)
  * [account\_history](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#изменения-в-плагине-accounthistory)
  * [operation\_history](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новый-плагин-operationhistory)
  * [social\_network](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#изменения-в-плагине-socialnetwork)
  * [tags](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новый-плагин-tags)
  * [follow](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#изменения-в-плагине-follow)
  * [database\_api](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#изменения-в-плагине-databaseapi)

## Перечень новых функциональных возможностей в HF•18

* Блокирование различного вида злоупотреблений делегированием Силы Голоса.
* Обеспечение более гибкой ценовой политики на бирже за счет удаления старых данных и использования актуальных в определении курса и соотношения крипто-валют.
* Возможность пользователям вносить изменения в профиль с использованием ключа posting.
* Возможность пользователям предлагать транзакцию на подписание, состоящей из нескольких операций. 
* Возможность пользователям вносить изменения в посты и комментарии независимо от срока их публикации и придавать им актуальность.

## Перечень новых технических возможностей в HF•18

* Повышение быстродействия системы за счет размещения в разных объектах полей с часто и редко используемыми данными.
* Повышение производительности API протокола за счет удаления неиспользуемых полей из методов плагинов, а также за счет перераспределения методов между плагинами для более эффективного их использования.
* Применение фильтрации тегов для настройки ленты в более удобной для пользователя форме.
* Возможность постраничного вывода личных сообщений на экран пользователя.

## Измененные и новые плагины в HF•18

### Изменения в плагине private\_message

В данный плагин добавлена возможность постраничного вывода списка личных сообщений. Изменены следующие методы \(шрифтом bold выделены добавленные аргументы\):

* get\_inbox\(string to, time\_point newest **, uint limit, uint offset**\)
* get\_outbox\(string from, time\_point newest **, uint limit, uint offset**\)

Метод `get_inbox` возвращает список входящих сообщений начиная с даты, заданной в newest.  
Метод `get_outbox` возвращает список исходящих сообщений начиная с даты, заданной в newest.  
`limit` — ограничивает количество сообщений \(максимально допустимое значение — 100\).  
`offset` — номер сообщения, с которого выполняется операция \(начиная с №\).

### Новый плагин witness\_api

Плагин `witness_api` образован перемещением части методов с часто используемыми полями из плагина `database_api`. В него вошли следующие методы:

* get\_current\_median\_history\_price
* get\_feed\_history
* get\_miner\_queue
* get\_witness\_schedule
* get\_witnesses
* get\_witness\_by\_account
* get\_witnesses\_by\_vote
* get\_witness\_count
* lookup\_witness\_accounts
* get\_active\_witnesses // &lt;- из выдаваемого результата удалены пустые строки

Все методы перемещены `в witness_api` без изменений во входных параметрах и выдаваемых результатах. Исключение составляет метод `get_active_witnesses`, у которого из выдаваемого результата удалены пустые строки.

### Изменения в плагине account\_history

Плагин `account_history` дополнен следующим методом:

* get\_account\_history

Метод перемещен из `database_api` без изменений во входных параметрах и выдаваемых результатах.

### Новый плагин operation\_history

Плагин `operation_history` образован перемещением методов из плагина `database_api`. Создание данного плагина позволяет отделить индексирование операций в блокчейне от истории пользователей. Пользователь может запрашивать и получать информацию об операциях в транзакциях \(блоках\) без ведения истории по аккаунтам. Это обеспечивает снижение нагрузки на сервер и на потребляемую память.

Плагин `operation_history` дополнен следующими методами:

* get\_ops\_in\_block
* get\_transaction

Методы перемещены из `database_api` без изменений во входных параметрах и выдаваемых результатах.

### Изменения в плагине social\_network

Часть методов из плагина `social_network` была перемещена во вновь созданный плагин `tags`. Перенос методов осуществлен для того, чтобы создание дополнительных индексов и поиск информации по ним проводились в отдельном плагине. В плагине `social_network` оставлены методы, обеспечивающие обращение к корневым элементам, а методы, обрабатывающие теги, перемещены в новый плагин `tags`.

Введен опциональный параметр `vote_limit` для задания максимального количества проголосовавших в ответе пользователю. По умолчанию его значение принимается равным 10000. Например, количество комментариев к посту может достигать 1000 и более, что затрудняет их просмотр и поиск интересующей информации. Пользователь может с использованием тэга сформировать запрос на получение комментариев, выбранных \(отсортированных\) в соответствии с указанными в тэге признаками. Параметр `vote_limit` позволяет уменьшить размер отправляемого от сервера ответа. При этом в ответе добавляется дополнительное поле `active_votes_count`, информирующее об общем количестве проголосовавших \(без необходимости получать полный список\).

Изменена результирующая структура:

```javascript
struct discussion {
    "active_votes_count": uint, // <— Добавлено. Общее количество голосов для vote_limit
      ...
}
```

Изменения внесены в методы, возвращающие структуру `discussion` и массив `discussion`. В этот перечень вошли следующие методы:

* get\_replies\_by\_last\_update\(string start\_parent\_author, string start\_permlink, uint limit `[, uint vote_limit]`\)
* get\_content\(string account, string permlink `[, uint vote_limit]`\)
* get\_content\_replies\(string author, string permlink `[, uint vote_limit]`\)
* get\_all\_content\_replies\(string author, string permlink `[, uint vote_limit]`\)
* get\_content\(string author, string permlink `[, uint32_t limit]`\)
* get\_active\_votes\(string account, string permlink `[, uint vote_limit]`\)
* get\_account\_votes\(string account `[, uint from, uint vote_limit]`\)

Фоном выделены параметры, которыми были дополнены методы.

Следующие методы, дублирующие функции плагина `tag`, были удалены из плагина `social_network`:

* get\_trending\_categories
* get\_active\_categories
* get\_recent\_categories
* get\_best\_categories

### Новый плагин tags

В плагин `tags` перемещены методы, выполняющие операции с тэгами \(например, получение наиболее популярных тэгов; получение списка языков; получение тэгов, используемых автором\). Это позволяет сэкономить размер файла разделяемой памяти тем пользователям, которые не используют данную функциональность.

Методы, которые перемещены из `social_network` без изменений:

* get\_trending\_tags\(string start, uint limit\)
* get\_languages\(\)
* get\_tags\_used\_by\_author\(string\)
* get\_discussions\_by\_payout\(query\)
* get\_discussions\_by\_trending\(query\)
* get\_discussions\_by\_created\(query\)
* get\_discussions\_by\_active\(query\)
* get\_discussions\_by\_cashout\(query\)
* get\_discussions\_by\_votes\(query\)
* get\_discussions\_by\_children\(query\)
* get\_discussions\_by\_hot\(query\)
* get\_discussions\_by\_feed\(query\)
* get\_discussions\_by\_blog\(query\)
* get\_discussions\_by\_comments\(query\)
* get\_discussions\_by\_promoted\(query\)

В метод `get_discussions_by_author_before_date` добавлен новый параметр `vote_limit` \(шрифтом bold выделен добавленный параметр\):

* get\_discussions\_by\_author\_before\_date\(string author, string start\_permlink, datetime before\_date, uint limit **\[, uint vote\_limit\]**\)

  ```javascript
  struct discussion_query {
        limit: uint,
        select_tags: [string],
        filter_tags: [string]
        select_languages: [string],
        filter_languages : [string],
        truncate_body: uint,
        vote_limit: uint,   // <— Новый параметр, по умолчанию принимает значение 10000 
        select_authors : [string],
        start_author: string,
        start_permlink: string,
        parent_author: string,
        parent_permlink: string
  }
  ```

  Изменена результирующая структура метода:

  ```javascript
  struct discussion {
     “reputation”: uint, // <- Поле отсутствует, если выключен плагин follow
    "active_votes_count": uint,   // <- Добавлено. Общее количество голосов для vote_limit
      ...
  }
  ```

### Изменения в плагине follow

В плагине `follow` изменена структура метода `get_account_reputations` в соответствии со следующим представлением:

* get\_account\_reputations\(array accounts\) 
  * Результат array

### Изменения в плагине database\_api

Плагин `database_api` дополнен новыми методами для выполнения новых операций.

Новые методы:

* [get\_proposed\_transaction](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новый-метод-getproposedtransaction)
* [get\_database\_info](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новый-метод-getdatabaseinfo)
* [get\_vesting\_delegations](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новый-метод-getvestingdelegations)
* [get\_expiring\_vesting\_delegations](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новый-метод-getexpiringvestingdelegations)  

Новые операции:

* [изменение или возврат делегирования Силы Голоса](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новая-операция-изменение-или-возврат-делегирования-силы-голоса)
* [создание аккаунта с делегированием Силы Голоса](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новая-операция-создание-аккаунта-с-делегированием-силы-голоса)
* [изменение json\_metadata  аккаунта](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новая-операция-изменение-jsonmetadata--аккаунта)
* [предложение на транзакцию](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новая-операция-предложение-на-транзакцию)
* [обновление предложенной транзакции](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новая-операция-обновление-предложенной-транзакции)
* [удаление предложенной транзакции](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новая-операция-удаление-предложенной-транзакции)
* [изменение параметров блокчейна](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новая-операция-изменение-параметров-блокчейна)

#### Неизменяемая часть database\_api

Часть методов из `database_api` перемещена в плагины `witness_api`, `account_history`, `operationt_history` и `follow`. Сохраненными в `database_api` без изменений остались следующие методы:

* get\_block\_header
* get\_block
* set\_block\_applied\_callback
* get\_config
* get\_dynamic\_global\_properties
* get\_chain\_properties
* get\_hardfork\_version
* get\_next\_scheduled\_hardfork
* get\_account\_count
* get\_owner\_history
* get\_recovery\_request
* get\_escrow
* get\_withdraw\_routes
* get\_account\_bandwidth
* get\_savings\_withdraw\_from
* get\_savings\_withdraw\_to
* get\_conversion\_requests
* get\_transaction\_hex
* get\_required\_signatures
* get\_potential\_signatures
* verify\_authority
* verify\_account\_authority
* lookup\_account\_names
* lookup\_accounts

### Изменения в методах database\_api

Поля `average_bandwidth` и `average_market_bandwidth` были удалены из плагина `database_api` как неиспользуемые. Заменяемые их в выполнении операций поля `new_average_bandwidth`, `new_average_market_bandwidth` были переименованы в первоначальные их имена `average_bandwidth` и `average_market_bandwidth` соответственно.

Поле `lifetime_bandwidth` было удалено и заменено на вновь созданное одноименное поле `lifetime_bandwidth`, зависящее от новых значений, а также поле `lifetime_market_bandwidth` для использования в маркетинговых операциях.

Из описания типа `bandwidth_type`, используемого в вызове метода `get_account_bandwidth`, удалены поля `old_forum` и `old_market`.

В поле `lifetime_bandwidth` хранится суммарное значение `bandwidth`, используемое аккаунтом за все время его работы. В поле `average_bandwidth` хранится среднее значение `bandwidth`, по которому определяется порог чрезмерной активности аккаунта.

#### Внесены изменения в выдаваемый результат следующего метода:

* get\_accounts

  ```javascript
  struct account {
    reputation, // <- Поле отсутствует, если выключен плагин follow
    transfer_history, // <- Удалено
    market_history, // <- Удалено
    post_history, // <- Удалено
    vote_history, // <- Удалено
    other_history, // <- Удалено
    tags_usage, // <- Удалено
    guest_bloggers, // <- Удалено
    blog_category, // <- Удалено
    ...
  }
  ```

  Удаление полей из структуры account обусловлено тем, что ранее эти поля никогда не использовались.

#### Новый метод get\_proposed\_transaction

Этот метод обрабатывает запрос на выдачу списка предложенных для подписания транзакций, поступивший от какого-либо аккаунта. Метод возвращает массив транзакций, в который входят транзакции, созданные непосредственно данным аккаунтом, а также транзакции, которые ему необходимо подписать.

* get\_proposed\_transaction\(account: string\)

  ```javascript
  struct proposal_object {
    author: string,
    title: string,
    memo: string,
    expiration_time: datetime,
    review_period_time: datetime, // может отсутствовать
    proposed_operations: [ operation ],
    required_active_approvals: [ string ],
    available_active_approvals: [ string ],
    required_owner_approvals: [ string ],
    available_owner_approvals: [ string ],
    required_posting_approvals: [ string ],
    available_posting_approvals: [ string ],
    available_key_approvals: [ string ]
  };
  ```

#### Новый метод get\_database\_info

Этот метод возвращает информацию о текущем статусе разделяемой памяти, в том числе: общий объем разделяемой памяти, размер свободного и зарезервированного пространства для определенных нужд, а также список индексов, хранящихся в разделяемой памяти \(название индекса, количество записей\).

* get\_database\_info\(\)

  ```text
  struct database_info {
    total_size: uint,
    free_size: uint,
    reserved_size: uint,
    used_size: uint

    index_list: [
            {
              name: string,
              record_count: uint
            },
    ]
  };
  ```

#### Новый метод get\_vesting\_delegations

Этот метод возвращает массив значений с описанием операции делегирования \(далее — блок делегирования\) аккаунта \(делегированный другим аккаунтам или же полученный от других аккаунтов\).

* get\_vesting\_delegations

  ```text
  get_vesting_delegations(
    string account,
    string from, uint32_t limit = 100,
    delegations type = delegated
  )
  ```

  `account` — аккаунт, по запросу от которого выдается блок делегирования. Отправитель\*/получатель определяется аргументом `type`.

  `from` — начальный аккаунт, парный в операции делегирования. Получатель/отправитель - задается аргументом `type` \(для пагинации\).

  `limit` — количество возвращаемых элементов \(для пагинации\). По умолчанию принимается равным 100. Максимальное значение равно 1000.

  `type` — тип запрашиваемого блока делегирования: "delegated" \(делегированный\), "received" \(полученный\). По умолчанию принимает значение "delegated".

Пример возвращаемого блока делегирования: `массив vesting_delegation_api_object [{id: 0, delegator: "zzz", delegatee: "zxcat", vesting_shares: "90.000000 GESTS", min_delegation_time: "2018-04-25T21:48:15"}]`.

#### Новый метод get\_expiring\_vesting\_delegations

Этот метод используется для получения списка возвращаемых \(отозванных и «замороженных»\) делегированных средств аккаунта. Метод возвращает результат в виде массива значений с описанием операции возврата делегированных средств \(далее — блок отозванного делегирования\)

* get\_expiring\_vesting\_delegations

  ```text
  get_expiring_vesting_delegations(
    string account,
    time_point_sec from,
    uint32_t limit = 100)
  ```

  `account` — аккаунт, возвращающий делегированные средства.

  `from` — начальное время возврата делегированных средств \(для пагинации\).

  `limit` — количество возвращаемых элементов \(для пагинации\). По умолчанию принимается равным 100. Максимальное значение равно 1000.

Пример возвращаемого модулем блока отозванного делегирования: `массив vesting_delegation_expiration_api_object, [{id: 0, delegator: "zxcat", vesting_shares: "123.000000 GESTS", expiration: "2018-05-25T11:18:45"}]`.

#### Новая операция: изменение или возврат делегирования Силы Голоса

Эта операция позволяет изменять количество делегированного, а также осуществлять возврат делегированного в полном объеме. Для выполнения этих операций необходима подпись ключом `active`. Операции выполняются с использованием следующей процедуры:

```javascript
delegate_vesting_shares
{
    delegator: string,    // делегирующий аккаунт
    delegatee: string,    // аккаунт-получатель
    vesting_shares: asset    // новое количество делегируемой Силы Голоса
}
```

Для выполнения этой опирации требуется подпись ключом `active`.

Для изменения количества делегирования Силы Голоса в поле `vesting_shares` следует задать новое значение. Для полного возврата делегированной части Силы Голоса в поле `vesting_shares` следует задать значение вида “0.000000 GESTS”. При изменении значения в сторону уменьшения делегированная Сила Голоса сразу снимется с аккаунта-получателя и переходит в «замороженное» состояние сроком на семь дней \(в случае создания аккаунта с делегированием этот период определяется параметром `create_account_delegation_time`\).

Минимальное количество Силы Голоса, необходимое для делегирования, определяется по результатам голосования делегатов.

#### Новая операция: создание аккаунта с делегированием Силы Голоса

Операция выполняется с использованием следующей процедуры:

```javascript
account_create_with_delegation
{
      fee: asset,        // комиссия, в GOLOS
      delegation: asset,    // делегируемая доля, в GESTS
      creator: string,        
      new_account_name: string,
      owner: authority,
      active: authority,
      posting, authority,
      memo_key: string,
      json_metadata: string,
      extensions: extensions_type    // Не используется, исходное значение — пусто
}
```

Для выполнения этой опирации требуется подпись ключом `active`.

Для создания аккаунта с делегированием необходимо, чтобы выполнялись следующие два условия:

```text
    1. fee ≥ create_account_min_golos_fee
    2. (delegation) ≥ (create_account_min_delegation)
```

где  
`fee` — размер комиссионных отчислений;  
`create_account_min_golos_fee` — минимальный размер комиссионных отчислений в криптовалюте Голос, требуемых на создание аккаунта с делегированием;  
`delegation` — делегированная часть Силы Голоса;  
`create_account_min_delegation` — минимальное количество Силы Голоса, необходимое для создания аккаунта с делегированием.

При создании аккаунта с делегированием бо́льшую часть комиссии можно оплатить с «заморозкой» на период, определяемый параметром `create_account_delegation_time`. Делегированная Сила Голоса может быть отозвана в любой момент \(например, в случае злоупотребления полученной делегированной частью новым аккаунтом\). При этом делегированная Сила Голоса будет снята с нового аккаунта сразу, а на делегирующий аккаунт будет возвращена по истечении срока «заморозки». Время «заморозки» является параметром, определяемым по результатам голосования. Его значение выбирается по медиане из списка всех значений, полученных от делегатов с помощью операции `chain_properties_update_operation`.

#### Новая операция: изменение json\_metadata  аккаунта

Пользователю предоставляется возможность изменять метаданные своего профиля без использования ключа `active`. Поля профиля хранятся в `json_metadata`. Для изменения любого поля профиля требовалась подпись только ключом `active`, что не всегда было приемлемым.

Было принято решение разделить поля на две группы. В состав первой группы вошли поля с наиболее значимыми данными профиля \(ключи: `posting`, `active`, `owner` и `memo`\), а в другую — с менее значимыми, но часто используемыми \(аватар, пол, местонахождение и пр.\). Процедура изменения полей первой группы сохранена и требует подписи только ключом `active`. В версии HF•18 вносить изменения в поля второй группы стало возможным с использованием ключа `posting` для подписи.

Операция выполняется с использованием следующей процедуры:

```javascript
account_metadata
{
    account: string,    // изменяемый аккаунт
    json_metadata: string    // новое значение json_metadata
}
```

Для выполнения этой опирации требуется подпись ключом `posting`.

#### Новая операция: предложение на транзакцию

Пользователю предоставляется возможность предлагать транзакцию на блокчейне с несколькими отдельными операциями, требующих одобрения от пользователей на их выполнение.

Операция выполняется с использованием следующей процедуры:

```javascript
proposal_create_operation
{
    author: string, // автор предлагаемой транзакции
    title: string,  // заголовок предложенной транзакции.
    memo: string,   // примечание
    proposed_operations: [ operation ], // список операций в предлагаемой транзакции
    expiration_time: datetime, // максимальное время, отведенное на транзакцию
    review_period_time: datetime, // время на принятие решения участников транзакции. Опциональный параметр
    extensions: extensions_type // расширение, по аналогии с другими операциями. Исходное значение — пусто
}
```

Для выполнения этой опирации требуется подпись ключом `active`.

Создаваемая транзакция должна быть уникальной по сочетанию полей author-title. По этой паре author-title идентифицируется транзакция в случае внесения в нее изменений или ее удаления.

В поле `proposed_operations` задается список операций для выполнения их в транзакции \(например, `{["delete_comment_operation":{"autor":"jim", "permlink":"hello"}}]`\). На каждую операцию из этого списка должна быть получена подпись автора, которому она предназначена. Право проставления подписи на выполнение любой операции из списка имеет также каждый из участников транзакции. Например, операция публикации поста назначается одному автору, а операция перечисления вознаграждения за нее — другому. В случае несогласия другого автора с выполнением второй операции он может удалить подпись на выполнение первой операции предложенной транзакции.

В поле `review_period_time` проставляется время, отводимое на принятие решений участников транзакции. Этот период должен быть меньше максимального времени из поля `expiration_time`, которое отводится на транзакцию. По истечении этого периода подписи в транзакции могут быть только удаляться.

Если параметр `review_period_time` не задан, то транзакция будет сразу выполняться после сбора всех необходимых подписей.

#### Новая операция: обновление предложенной транзакции

Автору, а также участникам транзакции, предоставляется возможность менять свое решение и обновлять подписи до истечения времени, отводимого на транзакцию.

Если транзакция не получает одобрения на выполнение какой-либо из операций, эта транзакция не отменяется и ее актуальность будет сохраняться до отведенного на ее выполнение времени. После получения всех необходимых подписей транзакция сразу будет выполняться и все последующие обновления будут считаться недействительными.

Операция выполняется с использованием следующей процедуры:

```javascript
proposal_update_operation
{
    author: string, // автор предложенной транзакции
    title: string,  // заголовок предложенной транзакции.
    active_approvals_to_add: [string], // список аккаунтов для подписи. Транзакция должна быть  
                    // подписана ключом active
    active_approvals_to_remove: [string], // список аккаунтов для удаления подписи из предложенной  
                    // транзакции. Транзакция должна быть подписана ключом active
    owner_approvals_to_add: [string], // список аккаунтов для подписи на операции в предложенной  
                    // транзакции. Транзакция должна быть подписана ключом owner
    owner_approvals_to_remove: [string], // список аккаунтов для удаления подписи из предложенной  
                    //транзакции. Транзакция должна быть подписана ключом owner
    posting_approvals_to_add: [string], // список аккаунтов для подписи на операции в предложенной  
                    // транзакции. Транзакция должна быть подписана ключом posting 
    posting_approvals_to_remove: [string], // список аккаунтов для удаления подписи из предложенной  
                    // транзакцию. Транзакция должна быть подписана ключом posting
    key_approvals_to_add: [string], // список ключей public для проставления подписей в предложенной  
                    // транзакции
    key_approvals_to_remove: [string], // список ключей public для удаления подписей из предложенной  
                    // транзакции
    extensions: extensions_type // расширение, по аналогии с другими операциями. Исходное значение — пусто
}
```

Подпись зависит от списка операций, предлагаемых на подписание.

По этой паре author-title идентифицируется транзакция в случае внесения в нее изменений или ее удаления. Поля, в которые записывается псевдоним для подписи транзакции, выбираются в зависимости от типа операций в предложенной транзакции.

#### Новая операция: удаление предложенной транзакции

В случае отказа кого-либо из участников транзакции в выполнении операции он может сформировать запрос на удаление предложенной транзакции. Идентификация транзакции осуществляется по паре author-title.

Операция выполняется с использованием следующей процедуры:

```javascript
proposal_delete_operation
{
    author: string, // автор предложенной транзакции
    title: string,  // заголовок предложенной транзакции
    requester: string, // псевдоним запросившего удаление транзакции или автор предложенной транзакции
    extensions: extensions_type // расширение, по аналогии с другими операциями. Исходное значение — пусто
}
```

Для выполнения этой опирации требуется подпись ключом `active`.

Удалить предложенную транзакцию может как ее автор, так и любой участник, от которого требуется подпись. Если хотя бы один из участников запрашивает удаление транзакции, то, независимо от подписей остальных участников, данная транзакция будет удалена.

#### Новая операция: изменение параметров блокчейна

Предыдущие версии блокчейна обеспечивают поддержку операции `witness_update`, которая позволяет делегатам Голоса изменять по результатам голосования значения следующих параметров:

* `account_creation_fee` — размер комиссионных отчислений, требуемых на создание аккаунта без делегирования;  
* `maximum_block_size` — максимальный размер блока блокчейна;  
* `sbd_interest_rate` — процент, начисляемый на SBD.  

Ввиду того, что `witness_update` не позволяет расширить перечень параметров, значения которых определяются голосованием, в версии HF•18 реализована новая операция `chain_properties_update`, которая поддерживает более расширенный перечень таких параметров и позволяет наращивать его в будущем. В версии HF•18 операция `chain_properties_update` поддерживает следующий перечень параметров, значения которых определяются голосованием:

* `account_creation_fee` — размер комиссионных отчислений, требуемых на создание аккаунта без делегирования;  
* `maximum_block_size` — максимальный размер блока блокчейна;  
* `sbd_interest_rate` — процент, начисляемый на SBD;  
* `create_account_min_golos_fee` — минимальный размер комиссионных отчислений в криптовалюте Голос, требуемых на создание аккаунта с делегированием \(по умолчанию принимает значение "1.000 GOLOS", см. операцию [account\_create\_with\_delegation](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новая-операция-создание-аккаунта-с-делегированием-силы-голоса)\);  
* `create_account_min_delegation` — устанавливает минимально возможное количество Силы Голоса при создании аккаунта с делегированием \(по умолчанию принимает значение "5.000 GOLOS", см. операцию [account\_create\_with\_delegation](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новая-операция-создание-аккаунта-с-делегированием-силы-голоса)\);  
* `create_account_delegation_time` — устанавливает минимально возможное время \(в секундах\) «заморозки» делегированной Силы Голоса при создании аккаунта с делегированием \(по умолчанию принимает значение за период в 30 дней, см. операцию [account\_create\_with\_delegation](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новая-операция-создание-аккаунта-с-делегированием-силы-голоса)\);  
* `min_delegation` — устанавливает минимально возможное количество Силы Голоса для делегирования на аккаунт \(по умолчанию принимает значение "10.000 GOLOS", см. операцию [delegate\_vesting\_shares](https://github.com/golos-blockchain/wiki/tree/d940af7f54725dd68c7f9080f07d5b5f609bf4d4/developers/hardforks/new_hardfork-hf18.md#новая-операция-изменение-или-возврат-делегирования-силы-голоса)\).  

Операция выполняется с использованием следующей процедуры:

```javascript
chain_properties_update_operation
{
     owner: string, // автор изменения
     props: {
       account_creation_fee: asset,
       maximum_block_size: uint,
       sbd_interest_rate: uint,
       create_account_min_golos_fee: uint,
       create_account_min_delegation: uint,
       create_account_delegation_time: uint,
       min_delegation: uint    
     }
}
```

Для выполнения этой опирации требуется подпись ключом `active`.

