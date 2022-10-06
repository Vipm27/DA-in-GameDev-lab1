# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #2 выполнил(а):
- Анофриев Данил Сергеевич
- ХПИ31
Отметка о выполнении заданий (заполняется студентом):

| Задание | Выполнение | Баллы |
| ------ | ------ | ------ |
| Задание 1 | * | 60 |
| Задание 2 | * | 20 |
| Задание 3 | * | 20 |

знак "*" - задание выполнено; знак "#" - задание не выполнено;

Работу проверили:
- к.т.н., доцент Денисов Д.В.
- к.э.н., доцент Панов М.А.
- ст. преп., Фадеев В.О.

[![N|Solid](https://cldup.com/dTxpPi9lDf.thumb.png)](https://nodesource.com/products/nsolid)

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

Структура отчета

- Данные о работе: название работы, фио, группа, выполненные задания.
- Цель работы.
- Задание 1.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 2.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Задание 3.
- Код реализации выполнения задания. Визуализация результатов выполнения (если применимо).
- Выводы.
- ✨Magic ✨

## Цель работы
познакомиться с программными средствами для организции
передачи данных между инструментами google, Python и Unity

## Задание 1
###Реализовать совместную работу и передачу данных в связке Python
- Google-Sheets – Unity. При выполнении задания используйте видео-материалы и
исходные данные, предоставленные преподавателя курса.
- В облачном сервисе google console подключить API для работы с google
sheets и google drive.
- Реализовать запись данных из скрипта на python в google-таблицу. Данные
описывают изменение темпа инфляции на протяжении 11 отсчётных периодов, с
учётом стоимости игрового объекта в каждый период.
- Создать новый проект на Unity, который будет получать данные из google-
таблицы, в которую были записаны данные в предыдущем пункте.

Задание выполнено, тесты проведены успешно, звук воспроизводиться.

![2022-10-05_20-02-25](https://user-images.githubusercontent.com/86101819/194130436-d6efd51b-5236-4fe5-b1e3-e53d462f1f40.png)
![2022-10-05_20-02-30](https://user-images.githubusercontent.com/86101819/194130434-e235fbc4-0a80-4aba-9551-4288ae144498.png)
![2022-10-05_20-02-34](https://user-images.githubusercontent.com/86101819/194130430-52c23caa-a7f6-49a2-9c60-18e9540cba36.png)
![2022-10-05_20-02-38](https://user-images.githubusercontent.com/86101819/194130425-1966a3c7-6c1a-44e4-9c9a-523890c3b8e2.png)
![2022-10-05_20-02-41](https://user-images.githubusercontent.com/86101819/194130445-35b8fc31-dea4-44df-804c-b081a7547e70.png)
![2022-10-05_19-38-31](https://user-images.githubusercontent.com/86101819/194130442-3a82b4c0-a08a-4274-8efd-887bcd0ef87d.png)
![2022-10-05_19-38-42](https://user-images.githubusercontent.com/86101819/194130438-c8a08cf4-1682-4fe5-9736-06c70ef52fa4.png)
![2022-10-05_20-39-58](https://user-images.githubusercontent.com/86101819/194130546-e7d4f767-0577-4a28-a7e0-d16aa219fba9.png)


## Задание 2
###Реализовать запись в Google-таблицу набора данных, полученных
с помощью линейной регрессии из лабораторной работы № 1

Сгенерировал новую гугл таблицу, код дописал
![2022-10-05_20-38-09](https://user-images.githubusercontent.com/86101819/194130925-b0d6c784-f82a-499f-801f-ca817fb80485.png)
![2022-10-05_20-38-16](https://user-images.githubusercontent.com/86101819/194130918-14fcb880-09ea-4511-863c-bb37a12bbe37.png)
![2022-10-05_20-38-20](https://user-images.githubusercontent.com/86101819/194130910-bd1b050b-3430-46bd-9e73-fa8ae1e9abb3.png)
![2022-10-05_20-38-24](https://user-images.githubusercontent.com/86101819/194130926-0aec3b8d-5478-4427-a44f-e63ff2c09100.png)
![2022-10-05_20-39-39](https://user-images.githubusercontent.com/86101819/194130996-83260d11-3eeb-413e-88a8-5ca1ccd95eaa.png)


## Задание 3
###Самостоятельно разработать сценарий воспроизведения звукового
сопровождения в Unity в зависимости от изменения считанных данных в задании 2

Переписал немного код на Unity, все работает
![2022-10-05_20-38-44](https://user-images.githubusercontent.com/86101819/194131540-e4350563-6709-42ae-9bf6-d0499124920e.png)
![2022-10-05_20-38-52](https://user-images.githubusercontent.com/86101819/194131533-e73b7ec8-4b21-47de-bdd6-bd31edc4bba5.png)
![2022-10-05_20-38-48](https://user-images.githubusercontent.com/86101819/194131538-2a231ea4-3543-4d7c-906e-47e86fac9c55.png)
![2022-10-05_20-38-56](https://user-images.githubusercontent.com/86101819/194131542-d2a17291-f5d5-4575-855c-e43836122a57.png)
![2022-10-05_20-39-58](https://user-images.githubusercontent.com/86101819/194131562-2c17079f-ea6e-429a-809f-4615e4f186b7.png)


## Выводы
Было интересно поработать с Unity, привязать это все к Таблице Гугл, поработать с Python. Я считаю, что у меня получилось справится с этим заданием, узнал много нового, разобрался в коде

| Plugin | README |
| ------ | ------ |
| Dropbox | [plugins/dropbox/README.md][PlDb] |
| GitHub | [plugins/github/README.md][PlGh] |
| Google Drive | [plugins/googledrive/README.md][PlGd] |
| OneDrive | [plugins/onedrive/README.md][PlOd] |
| Medium | [plugins/medium/README.md][PlMe] |
| Google Analytics | [plugins/googleanalytics/README.md][PlGa] |

## Powered by

**BigDigital Team: Denisov | Fadeev | Panov**
