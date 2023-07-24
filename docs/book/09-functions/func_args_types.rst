.. meta::
   :http-equiv=Content-Type: text/html; charset=utf-8

Типы аргументов функции
-----------------------

При вызове функции аргументы можно передавать двумя способами:

* как **позиционные** - передаются в том же порядке, в котором они определены
  при создании функции. То есть, порядок передачи аргументов определяет, 
  какое значение получит каждый аргумент
* как **ключевые** - передаются с указанием имени аргумента и его значения.
  В таком случае, аргументы могут быть указаны в любом порядке, так как их имя указывается явно.

.. image:: https://raw.githubusercontent.com/natenka/pyneng-book/master/images/09_function_args.png
   :align: center
   :class: only-light

.. only:: html

    .. image:: https://raw.githubusercontent.com/natenka/pyneng-book/master/images/09_function_args_dark.png
       :align: center
       :class: only-dark

Позиционные и ключевые аргументы могут быть использоваться одновременно при вызове функции.
При этом сначала должны идти позиционные аргументы, а только потом - ключевые.

Посмотрим на разные способы передачи аргументов на примере функции
check_passwd (файл func_check_passwd_optional_param.py):

.. code:: python

    def check_passwd(username, password):
        if len(password) < 8:
            print('Пароль слишком короткий')
            return False
        elif username in password:
            print('Пароль содержит имя пользователя')
            return False
        else:
            print(f'Пароль для пользователя {username} прошел все проверки')
            return True


Позиционные аргументы
~~~~~~~~~~~~~~~~~~~~~

Позиционные аргументы при вызове функции надо передать в правильном
порядке (поэтому они и называются позиционные).

.. code:: python

    In [2]: check_passwd('nata', '12345')
    Пароль слишком короткий
    Out[2]: False

    In [3]: check_passwd('nata', '12345lsdkjflskfdjsnata')
    Пароль содержит имя пользователя
    Out[3]: False

    In [4]: check_passwd('nata', '12345lsdkjflskfdjs')
    Пароль для пользователя nata прошел все проверки
    Out[4]: True

Если при вызове функции поменять аргументы местами, скорее всего,
возникнет ошибка, в зависимости от конкретной функции.

Ключевые аргументы
~~~~~~~~~~~~~~~~~~

**Ключевые аргументы**:

* передаются с указанием имени аргумента
* за счет этого они могут передаваться в любом порядке

Если передать оба аргумента как ключевые, можно передавать их в любом
порядке:

.. code:: python

    In [9]: check_passwd(password='12345', username='nata', min_length=4)
    Пароль для пользователя nata прошел все проверки
    Out[9]: True


.. warning::
    Обратите внимание, что всегда сначала должны идти позиционные
    аргументы, а затем ключевые.

Если сделать наоборот, возникнет ошибка:

.. code:: python

    In [10]: check_passwd(password='12345', username='nata', 4)
      File "<ipython-input-10-7e8246b6b402>", line 1
        check_passwd(password='12345', username='nata', 4)
                                                       ^
    SyntaxError: positional argument follows keyword argument


Но в такой комбинации можно:

.. code:: python

    In [11]: check_passwd('nata', '12345', min_length=3)
    Пароль для пользователя nata прошел все проверки
    Out[11]: True

В реальной жизни зачастую намного понятней и удобней указывать
флаги (параметры со значениями True/False) или числовые значения как ключевой аргумент. Если
задать хорошее название параметра, то по его имени сразу
будет понятно, что именно он делает.

Например, можно добавить флаг, который будет контролировать, выполнять проверку наличия имени пользователя в пароле или нет:

.. code:: python

    def check_passwd(username, password, min_length=8, check_username=True):
        if len(password) < min_length:
            print('Пароль слишком короткий')
            return False
        elif check_username and username in password:
            print('Пароль содержит имя пользователя')
            return False
        else:
            print(f'Пароль для пользователя {username} прошел все проверки')
            return True


По умолчанию флаг равен True, а значит проверку выполнять надо:

.. code:: python

    In [14]: check_passwd('nata', '12345nata', min_length=3)
    Пароль содержит имя пользователя
    Out[14]: False

    In [15]: check_passwd('nata', '12345nata', min_length=3, check_username=True)
    Пароль содержит имя пользователя
    Out[15]: False

Если указать значение равным False, проверка не будет выполняться:

.. code:: python

    In [16]: check_passwd('nata', '12345nata', min_length=3, check_username=False)
    Пароль для пользователя nata прошел все проверки
    Out[16]: True
