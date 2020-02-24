---
description: ...
---

# API part 3

Автор: [@asuleymanov](https://golos.io/@asuleymanov)

Приветствую постоянных читателей и вновь присоединившихся.  
В предыдущей [статье](https://golos.io/ru--otkrytyij-kod/@asuleymanov/opisani-golosapi-chast-2) я завершил описание API команд из раздела Database\_API. Осталось еще 3 раздела. В данной статье я постараюсь описать 2 из 3 раздела, а именно Market\_History\_API и Follow\_API.  
Последний раздел NetworkBrodcast\_API я оставлю на финал \(как самое вкусное и желанное\), пусть будет в виде вишенки на торте.

Оба раздела включенных в данную публикацию не содержат большого количества команд. Но от этого они не менее важны.

Приступим.

## Market\_History\_API

В данном разделе содержатся команды для получения данных о операциях проводимых на внутренней бирже сети.

_**get\_ticker**_  
Параметры:`"method":"get_ticker", "params":[], "id":0`  
Описание: Возвращает рыночный тикер для внутреннего рынка GBG:GOLOS.

_**get\_volume**_  
Параметры:`"method":"get_volume", "params":[], "id":1`  
Описание: Возвращает объем рынка за последние 24 часа.

_**get\_order\_book**_  
Параметры:`"method":"get_order_book", "params":["limit"], "id":2`  
Описание: Отображает список заявок на внутренней бирже на покупку и продажу в сети GOLOS.

_**get\_trade\_history**_  
Параметры:`"method":"get_trade_history", "params":["start","end","limit"], "id":3`  
Описание: Возвращает историю торговли для внутреннего рынка GBG:GOLOS.  
start - время начала торговой истории  
end - время окончания торговой истории

_**get\_recent\_trades**_  
Параметры:`"method":"get_recent_trades", "params":["limit"], "id":4`  
Описание: Возвращает N последних сделок для внутреннего рынка GBG:GOLOS.

_**get\_market\_history**_  
Параметры:`"method":"get_market_history", "params":[["bucket_seconds","start","end"]], "id":5`  
Описание: Возвращает историю для внутреннего рынка GBG:GOLOS.  
bucket\_seconds - размер стакана\(среза\) в секундах  
start - время начала торговой истории  
end - время окончания торговой истории

_**get\_market\_history\_buckets**_  
Параметры:`"method":"get_market_history_buckets", "params":[], "id":6`  
Описание: Возвращает размер секунд стакана\(среза\), отслеживаемых плагином.

В последних двух командах использовано слово стакан\(срез\). Я к сожалению не биржевой человек и не сильно понимаю все её хитрости. Поэтому если кто то сможет это разъяснить буду очень этому признателен.

## Follow\_API

Данный раздел позволяет получить данные о подписках, подписчиках и репостах пользователей.

_**get\_followers**_  
Параметры:`"method":"get_followers", "params":["following","startFollower","follow_type","limit"], "id":0`  
Описание: Возвращает список:  
Либо всех подписчиков пользователя "following".  
Либо если указано имя пользователя в параметре "startFollower" возвращается список совпадающих подписчиков.  
Параметр "follow\_type" может принимать только такие строковые значения \(undefined,blog,ignore\)

_**get\_following**_  
Параметры:`"method":"get_following", "params":["follower","startFollower","follow_type","limit"], "id":1`  
Описание: Как я понимаю.\(К сожалению никакие попытки получить результата успехом не увенчались\)  
Возвращает список:  
Либо всех на кого подписан пользователь "follower".  
Либо если указано имя пользователя в параметре "startFollower" возвращается список совпадающих пользователей на которых они подписаны.  
Параметр "follow\_type" может принимать только такие строковые значения \(undefined,blog,ignore\)

_**get\_follow\_count**_  
Параметры:`"method":"get_follow_count", "params":["username"], "id":2`  
Описание: Возвращает данные о количестве подписчиков и подписок указанного пользователя.

_**get\_feed\_entries**_  
Параметры:`"method":"get_feed_entries", "params":["account","entry_id","limit"], "id":3`  
Описание: Возвращает краткие данные о записях из ленты указанного пользователя.  
Параметр "entry\_id" установленный в 0 выдает самые свежие данные.

_**get\_feed**_  
Параметры:`"method":"get_feed", "params":["account","entry_id","limit"], "id":4`  
Описание: Возвращает полные данные о записях из ленты указанного пользователя.  
Параметр "entry\_id" установленный в 0 выдает самые свежие данные.

_**get\_blog\_entries**_  
Параметры:`"method":"get_blog_entries", "params":["account","entry_id","limit"], "id":5`  
Описание: Возвращает краткие данные о записях из блога указанного пользователя.  
Параметр "entry\_id" установленный в 0 выдает самые свежие данные.

_**get\_blog**_  
Параметры:`"method":"get_blog", "params":["account","entry_id","limit"], "id":6`  
Описание: Возвращает полные данные о записях из блога указанного пользователя.  
Параметр "entry\_id" установленный в 0 выдает самые свежие данные.

_**get\_account\_reputations**_  
Параметры:`"method":"get_account_reputations", "params":["lowerBoundName","limit"], "id":7`  
Описание: Возвращает данные о репутации пользователей отфильтрованных по шаблону.

_**get\_reblogged\_by**_  
Параметры:`"method":"get_reblogged_by", "params":["author","permlink"], "id":8`  
Описание: Возвращает список пользователей которые либо создали запись либо сделали её репост.

_**get\_blog\_authors**_  
Параметры:`"method":"get_blog_authors", "params":["username"], "id":9`  
Описание: Возвращает список авторов и количество репостов этого автора пользователем.
