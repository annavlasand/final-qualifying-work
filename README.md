# final-qualifying-work\n
Выпускная квалификационная работа по курсу «Инженер данных (Data engineer Pro)»
Выполнила Власенкова Анна Андреевна
Задача: необходимо на основе данных с ftp.zakupki.gov.ru научиться определять группу, к которой относится контракт с кодом ОКПД-2 41, 42, 43, 71.1.

Группы могут быть следующими:

1. Строительно-монтажные работы (СМР)
2. Проектно-изыскательские работы (ПИР)
3. Строительный надзор
4. Подключение коммуникаций
5. Прочее.
По ОКПД-2 контракты в общем случае должны разделяться так: Строительно-монтажные работы (СМР) - 41, 42, 43(кроме нижеперечисленных) Проектно-изыскательские работы (ПИР) - 41.1, 71.1 Подключение коммуникаций - 43.22 Строительный надзор – четкой группы нет.

Проблема: Далеко не всегда контракты указываются с нужным кодом, поэтому есть проблема как такие контракты "отловить" и определить в нужную группу.

Поэтому задача предполагает классификацию контрактов на основе объекта закупки, который сформулирован естественным языком. На основе этого на входе данные о контрактах. На выходе необходимо получить группу для каждого контракта.

Иногда контракт может относиться одновременно в несколько групп.

1. Загрузка csv файла объемом 25Гб. Предложена модель загрузки данных в базу данных с последующим извлечением для анализа.
2. Проведение разведочного анализа данных. Датасет был исследован на предмет поиска нужных столбцов согласно шаблону, исследовались его различные характеристики.
3. Проведена предобработка датафрейма и приведение его к удобному виду для последующей обработки NLP
4. Проведена обработка значений объекта закупки с помощью средств NLP (токенизация, стемминг, очистка от ненужных символос и стоп-слов)
5. В качестве разметки решено принять правильными номера групп ОКПД, так как явно разметка в датасете не прослеживается, необходимо узнавать такие сведения у заказчика
6. Проведена классификация различными моделями с последующей настройкой гиперпараметров для улучшения точности предсказаний классов.
   Анализировались следующие модели:
   логистическая регрессия
   случайны лес
   к ближаших соседей

Вывод:

В ходе проведения исследования была проведена классификация контрактов по группам ОКПД алгоритмами логистической регрессии, "случайного леса" и k ближайших соседей.
Для модели логистической регрессии проводился подбор оптимальных гиперпараметров с помощью GridSearchCV.
Учитывая, что мы опирались на гипотезу о правильности расстановки кодов ОКПД для определения разметки данных, а это с большой вероятностью не всегда так, необходимо уточнить информацию по разметке у заказчика
и повторить исследование с правильной разметкой.
В результате лучше всего себя показал классификатор "случайный лес" с точностью 0,93.
