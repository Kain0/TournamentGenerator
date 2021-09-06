# TournamentGenerator

Исходники плагина для генерации турниров вида PlayOff и RoundRobin на Unreal Engine 4 (UE4).
Разработан Неугодниковым С.И. и Поповым А.Э.

Проект на стадии в альфа тестирования. Поэтому если вы найдете какой-либо баг или недочет, то напишите нам (Telegram: @Azzazzin892 - Неугодников С.И.; @Kaino0 - Попов А.Э.).
Мы будем рады вашему сообщению и попытаемся устранить неполадки.

## Установка

Ссылка на билд: https://drive.google.com/drive/folders/1ZQJISYF7LsMoSptDKsxjTppCNx09W0Qw?usp=sharing

Необходимо распаковать архив и поместить папку TournamentGenerator в папку Plugins основного проекта (Папка Plugins должна находится на одном уровне файлом .uproject, нужно будет создать папку Plugins, если её нет).
Далее в UE4 необходимо убедится, что в окне плагинов у плагина TournamentGenerator стоит галочка Enabled.

После описанных действий должна появится возможность использования компонентов, которые предоставляет плагин.

## Документация

Плагин доступен для исползования в Blueprints. Доступные виды турниров представлены компонентами:
UPlayOffTournamentComponent и URRTournamentComponent.

#### PlayOffTournamentComponent

  ##### GenerateTournament 
  Генерирует турнир. Необходимо сообщить список id участников турнира и список их рейтингов. А также необходимо выбрать тип генерации турнира.

  Вообще говоря, для турнира на выбывание требуется число игроков, равное степени двойки. Поэтому если число игроков не равно степени двойки - первый этап турнира уменьшит число     игроков до степени двойки.  Некоторые игроки при этом не будут участвовать в первом этапе.

  ##### типы генерации:
  
  Random - случайная генерация турнирной сетки.
  
  WorstAgainstBest - Слабый игрок будет играть против сильного. Например для игроков с рейтнгами: 1,2,3,4,5,6,7,8 будут составлены следующие матчи: 1 vs 8, 3 vs 6, 4 vs 5, 2 vs 7

  Directly - Посланный список игроков будет использован напрямую без каких-либо изменений. Для игроков с id: 1, 2, 3, 4. Будут составлены следующие матчи: 1 vs 2, 3 vs 4.
    
  ##### ChooseWinner
  Устанавливает победителя в матче. Необходимо сообщить id игрока. Если id не будет найден, то изменений не произойдёт.
  
  ##### NextStage
  Переводит турнир на следующий этап, если победители во всех матчах текущего этапа определены. Возвращет bool - удалось ли перейти на следующий этап.
  
  ##### GetMatchByIndex
  Возвращает информацию о матче текущего этапа в виде структуры типа FMatch. Необходимо сообщить индекс матча.
  
  ##### GetMatchCount
  Возвращает число матчей на текущем этапе.
  
  ##### GetCurrentStageIndex
  Возвращает индекс тукущего этапа.
  
  ##### IsTournamentFinished
  Возвращает bool - закончился ли турнир. Турнир считается законченным, если определён финальный победитель.
  
  ##### GetWinners

  Возвращает список победителей на последнем законченном этапе.
  
  ##### GetWinnersByStageIndex
  
  Возвращает список победителей этапа по индексу этого этапа.
  
  ##### GetCurrentStageMembers
  
  Возвращает список участников текущего этапа. В него не попадают участиники с автоматической победой, когда у низ нет соперника.
  
  ##### SetMemberStatus
  
  Устанавливает статус участнику по его id: Active или NotActive. Участникам со статусом NotActive автоматически присваивается поражение. Если в матче оба участника имеют такой
  статус - оба считаются проигравшими и ни один из них не попадает в следующий этап.
  
  ##### RandomizeWinners

  Выбирает победителей случайным образом на каждом этапе.
  
  ##### PrintTournamentInfo
  
  Пишет в лог информацию и матчах.
  
  ##### SaveJson
  
  Сохраняет турнир в json-формате в папку Content основного проекта. Необходимо ввести название файла.
  
  ##### LoadJson
  
  Загружает новые данные турнира из файла в формате json.
  
 #### PlayOffTournamentComponent
 
  ##### GenerateNewTournament
  Генерирует турнир и возвращает информацию о нем. Для корректной генерации нужно послать массив id участников, массив очков рейтинга, длинна которого должна совпадать с длинной массива участиков, и выбрать один из типов генерации турнирной сетки.
  
  ##### типы генерации:
  
  RoundMethod - генерация турнирной сетки, в котором противники в каждом раунде меняются по кругу.
  
  BergerTables - генерация турнирной сетки методом "Berger Tables" (описание: https://en.wikipedia.org/wiki/Round-robin_tournament)
 
 ##### GetAllMatchesInfo
 
 Возвращает информацию о все матчах (номер матча; кто с кем сражается; состояние матча).
 
 ##### виды состояния матча:
 
 1) Матч не окончен;
 2) Победил игрок с id...;
 3) Матч пропущен из-за наличия только одного игрока.
 
 ##### GetWinStatistics
 
 Возвращает информацию о игроках и количеством выйгранных ими матчами. Отсортированны в порядке убывания количества выйгранных матчей.
 
 ##### GetAllMembersInfo
 
 ##### GetMemberInfoByMemberIndex
 
 ##### GetMatchInfoByMatchNumber
 
 ##### SetAllWinners
 
 ##### SetWinnerByMatchNumber
 
 ##### SetAllRatingPoints
  
 ##### SetRatingPointsByMemberIndex
 
 ##### DisqualificationByMemberIndex
 
 ##### GetMatchesCount
 
 ##### ChooseWinner
 
 ##### IsOnePersonOnFirstPlace
 
 ##### GenerateExtraMatches
 
 ##### SaveJson
 
 ##### LoadJson
 
TO BE CONTINUED
