FIXME: Нужно переработать нумерацию так, чтобы в новой версии она сохранилась
надолго и хорошо выдерживала бы расширения и изменения документа.

Приоритеты
==========

* Читаемость кода (в том числе единообразие).
* Уменьшение вероятности возникновения ошибок.
* Минимизация числа изменённых строк с точки зрения системы контроля версий при модификации кода.
* Производительность кода.

Пробельные символы
==================

В коде нельзя использовать символы табуляции (кроме мэйкфайлов). Если в
строковом литерале нужен символ табуляции, используйте "\t".

Строки желательно ограничивать теми кавычками, которых нет в тексте: `'"'`, а не
`"\""`; `"'"`, а не `'\''`; `[["']]`, а не `"\"'"`.

В коде нужно использовать отступы шириной два пробела ("единичный отступ"),
кроме кода, который будет использоваться внутри Metalua. Такой код нужно
обозначить в комментариях в начале файла, и использовать отступы в три пробела.

В конце строки не должно быть пробельных символов.

Максимальная длина строки — 80 символов. 

Нельзя ставить подряд больше одного пробела (кроме как для отступов в начале
строки и между "столбцами" в "табличных" данных).

Нельзя делать подряд больше одной пустой строки.

После каждой запятой и точки с запятой должен стоять пробел. Перед запятой и
точкой с запятой — не должно быть пробела.

Все бинарные операторы (=, ~=, <, >, +, -, *, /, and, or, ..)  должны отделяться
пробелами слева и справа.

Оператор # и унарный минус не отделяются пробелом от операнда, но отделяются
пробелом слева.

Оператор not отделяется пробелами слева и справа.

Нельзя отделять пробелами скобки при вызове функций (кроме специальных
декларативных форм записи).

После открывающей и перед закрывающей скобками пробел не ставится.

После открывающей фигурной скобки и перед закрывающей фигурной -- ставится.

Файл должен завершаться символом перевода строки.

Тело и заголовок неанонимной функции, занимающие вместе более одной строки
должны отделяться пустыми строками до и после.

Правила расстановки отступов
============================

FIXME: Нужны примеры! Пока — смотрите на код. -Alexander Gladysh 24.11.09 22:55 

По умолчанию следует избегать разницы в отступах на соседних непустых строках
большей чем в один отступ (кроме специально оговорённых случаев).

При "разрыве" выражения и переносе части его на следующую строку в ней делается
один дополнительный отступ (кроме специально оговорённых случаев). Если
выражение разбито на несколько строк, все строки кроме самой первой начинаются с
одного дополнительного отступа.

К примеру:
    assert(
        action_handlers[action.tool],
        "unknown tool"
      )(
        manifest,
        cluster_info,
        param,
        machine,
        role_args,
        action
     )

    machine.installed_rocks_set, machine.duplicate_rocks_set 
        = luarocks_parse_installed_rocks(
            remote_luarocks_list_installed_rocks(
                machine.external_url
            )
        )

    writeln_flush(
        "-> blablablablablablablablablabla "
    .. blabla_blabla
    .. "': blablablablablablablablablabla"
    )

    longname_a = longname_b 
      [logic_operand] longname_c

    if
       long_function_name(
             with, 
             many, 
             many, 
             parameters
         ) == other_long_function(
             the, 
             same
         )
    then
      body
    end

    local func_name = function(
        param1,
        param2,
        longname3
      )
      body
    end

В табличных, столбчатых и прочих подобных данных допускается расстановка
отступов по необходимости для сохранения столбцов, если это повышает читаемость.

При многострочной записи код внутри, function-end, do-end, then-end,
repeat-until и подобных конструкций сдвигается вправо на один отступ.

При многострочной записи конструктора таблицы, открывающая и закрывающая
фигурные скобки пишутся на новых строках с отступом, равным отступу первой
непустой строки перед открывающей скобкой.

Допускается сдвиг вправо на один отступ кода, находящегося между
begin()-end()-подобными парными конструкциями.

При разделении вызова функции на несколько строк, аргументы функции сдвигаются
на ДВА отступа, закрывающая скобка — на один относительно строки с
открывающей. Открывающую скобку желательно ставить на той же строке, что и имя
функции. Желательно в этом случае писать каждый аргумент функции на новой
строке. Отступы в объявлении функции оформляются аналогично.

Если при вызове функции ей передаётся единственный аргумент, и этот аргумент —
анонимная функция, создаваемая конструкцией function-end непосредственно в
момент вызова, тело функции сдвигается на ОДИН отступ (а не на два). Ключевое
слово function пишется непосредственно после открывающей скобки вызова, без
пробела между ними. Соответствующее ключевому слову function ключевое слово end
пишется с тем же отступом, что и строка, на которой написано
function. Закрывающая скобка вызова ставится непосредственно после end-а, без
пробела между ними. Допускается запись в одну строку: foo(function(args) body()
end)

FIXME: Нужно описать: import, return and or, нестандартный сдвиг влево при
конкатенации, многострочное условие if-then while-do for-do, (что ещё?!)
-Alexander Gladysh 24.11.09 22:56

Избыточный синтаксис
====================

Нельзя ставить скобки вокруг условия в if-then, while-do, for-do, repeat-until.

Синтаксический сахар
====================

Если функция не рекурсивная, используется форма определения a = function() end.

Если функция рекурсивная -- function a() end.

При вызове методов нужно пользоваться оператором ":".

Нельзя опускать скобки при передаче строковых литералов и конструкторов таблиц в
качестве аргументов функций, если код написан в императивном стиле.

В коде, написанном в декларативном стиле, желательно опускать скобки при
передаче строковых литералов и конструкторов таблиц в качестве аргументов
функций. (В т. ч. "import".)

Заголовки функций
=================

Конструкторы таблиц
===================

Если таблица создаётся на одной строке, желательно отделять её элементы
запятыми.

Если таблица создаётся на нескольких строках, желательно отделять её элементы
точками с запятой, и располагать по одному элементу на строке.

Нельзя смешивать запятые и точки с запятой в одном списке.

Если список разделён запятыми, в конце списка "висящая" запятая не ставятся.

Если список разделён точками с запятой, в конце списка также ставится точка с
запятой.

Пример:
    local ks = { "k1", "k2", "k3" }

    local items =
    {
      "item1";
      "item2";
      "item3";
    }

Видимость переменных
====================

Область видимости переменных должна быть максимально ограничена, насколько
позволяет здравый смысл в каждой конкретной ситуации.

Глобальные переменные запрещены (кроме специальных случаев). Любой случай
введения новой глобальный переменной должен утверждаться отдельно и
документироватья в коде.

Видимость переменных в глобальном scope файла следует максимально ограничивать
блоками do-end.

Не следует повторно использовать одну и ту же переменную для разных целей (кроме
документированных случаев, где это необходимо из-за сверхжёстких требований по
производительности — на практике таких случаев пока не было).

Имена переменных не должны перекрывать имена переменных во внешних scope'ах
(допускаются обоснованные исключения, например в случаях, когда это улучшает
читаемость кода).

Стандартные глобальные переменные (например, print, error) желательно
"кешировать" в локальные в начале файла: local print, error = print, error. Это
позволяет создать код, который будет без "из коробки" работать внутри sandbox'а
с заменённым глобальным окружением.

Описание объектов
=================

Следует придерживаться следующего формата.

FIXME: Раскрыть; описать варианты с метатаблицами и upvalue как допустимые, и случаи, в которых они предпочтительны.)

    local make_myobject
    do
      local method = function(self, args)
      end
      
      make_myobject = function(args)
        return
          {
            method = method;
            --
            private_variable_ = 42;
          }
      end
    end

Поля таблицы с подчеркиванием в конце - приватные данные.

Модули
======

Разделение кода на файлы
========================

Общая культура программирования
===============================

В коде следует избегать использования безымянных "магических констант":
http://en.wikipedia.org/wiki/Magic_number_(programming)#Unnamed_numerical_constants

Именование переменных
=====================

Никакой "венгерской нотации".

Константы именуются ЗАГЛАВНЫМИ_БУКВАМИ.

Обычные переменные, имена функций и проч. — через_подчёркивание, без заглавных букв.

Имя переменной, обычно, существительное.

Имя переменной, содержащей объект должно содержать название этого объекта
(см. XIV.3. Фабрики). (Обычно такая переменная — таблица.)

Имя переменной (таблицы), содержащей в себе коллекцию объектов обычно содержит
существительное во множественном числе (foos — коллекция объектов foo).

Линейные коллекции (в смысле ipairs) допускается называть с суффиксом _list в
случаях, когда нужно особо подчеркнуть линейность.

Имя булевой переменной, обычно, is_* (are_*, has_* и проч. формы to be), have_*,
need_*, should_*, must_*, in_*, not_* и т.п.

Количество объектов: num_*.

Именование функций
==================

Имя функции должно заключать в себе глагол либо заканчиваться на существительное
с окончанием -er (чаще всего когда подразумевается "функтор"), кроме специальных
случаев и декларативного кода.

Предикаты: is_<verb>
Фабрики: make_<object_name>
