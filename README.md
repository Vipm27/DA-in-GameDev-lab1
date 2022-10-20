# АНАЛИЗ ДАННЫХ И ИСКУССТВЕННЫЙ ИНТЕЛЛЕКТ [in GameDev]
Отчет по лабораторной работе #3 выполнил(а):
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
###Реализовать систему машинного обучения в связке Python - Google-Sheets – Unity.
1 Создим на сцене плоскость, шар и куб и изменим их цвета

![2022-10-12_15-28-30](https://user-images.githubusercontent.com/86101819/196964812-942380e4-0eb7-46f6-b4c7-c9d4c76fd7a7.png)
2 Добавим сфере скрипт RollerAgent.cs
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;
using Unity.MLAgents.Actuators;

public class RollerAgent : Agent
{
    Rigidbody rBody;
    // Start is called before the first frame update
    void Start()
    {
        rBody = GetComponent<Rigidbody>();
    }

    public Transform Target;
    public override void OnEpisodeBegin()
    {
        if (this.transform.localPosition.y < 0)
        {
            this.rBody.angularVelocity = Vector3.zero;
            this.rBody.velocity = Vector3.zero;
            this.transform.localPosition = new Vector3(0, 0.5f, 0);
        }

        Target.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
    }
    public override void CollectObservations(VectorSensor sensor)
    {
        sensor.AddObservation(Target.localPosition);
        sensor.AddObservation(this.transform.localPosition);
        sensor.AddObservation(rBody.velocity.x);
        sensor.AddObservation(rBody.velocity.z);
    }
    public float forceMultiplier = 10;
    public override void OnActionReceived(ActionBuffers actionBuffers)
    {
        Vector3 controlSignal = Vector3.zero;
        controlSignal.x = actionBuffers.ContinuousActions[0];
        controlSignal.z = actionBuffers.ContinuousActions[1];
        rBody.AddForce(controlSignal * forceMultiplier);

        float distanceToTarget = Vector3.Distance(this.transform.localPosition, Target.localPosition);

        if(distanceToTarget < 1.42f)
        {
            SetReward(1.0f);
            EndEpisode();
        }
        else if (this.transform.localPosition.y < 0)
        {
            EndEpisode();
        }
    }
}
```
3. Добавим сфере Decision Requester и Behavior Parameters
4. В корень проекта добавим файл конфигурации нейронной сети и запустим работу ml-агена
![2022-10-12_15-31-23](https://user-images.githubusercontent.com/86101819/196965599-15809194-8b1b-4439-a0b5-7658d39e24e7.png)
5. Сделаем несколько копий модели TargetArea, и обучим их!
[2022-10-12_15-28-49](https://user-images.githubusercontent.com/86101819/196966018-50eed43a-ff17-4f22-b68d-e59532c8870c.png)
![2022-10-12_15-32-05](https://user-images.githubusercontent.com/86101819/196965768-5367dbdd-2b27-42ed-8713-86441754f074.png)
6.Модель совершенно исправно работает, шар обучается, двигается
## Задание 2
###Подробно описать каждую строку файла конфигурации нейронной сети. Самостоятельно найти информацию о компонентах Decision Requester, Behavior Parameters, добавленных сфере.
```cs
behaviors:
  RollerBall: # указываем id агента
    trainer_type: ppo # режим обучения (Proximal Policy Optimization)
    hyperparameters:
      batch_size: 10 # количество опытов на каждой итерации
      buffer_size: 100 # количество опыта, которое нужно набрать перед обновлением модели
      learning_rate: 3.0e-4 # начальная скорость обучения
      beta: 5.0e-4 # сила регуляции энтропии, увеличивает случайность действий
      epsilon: 0.2 # порог расхождений между старой и новой политиками при обновлении
      lambd: 0.99 # параметр регуляции, насколько сильно агент полагается на текущий value estimate
      num_epoch: 3 # количество проходов через буфер опыта, при выполнении оптимизации
      learning_rate_schedule: linear # определяет как скорость обучения изменяется с течением времени
                                     # linear линейно уменьшает скорость
    network_settings:
      normalize: false # отключаем нормализацию входных данных
      hidden_units: 128 # количество нейронов в скрытых слоях сети
      num_layers: 2 # количество скрытых слоёв в сети
    reward_signals:
      extrinsic:
        gamma: 0.99 # коэффициент скидки для будущих вознаграждений
        strength: 1.0 # коэффициент на который умножается вознаграждение
    max_steps: 500000 # общее количество шагов, которые должны быть выполнены в среде до завершения обучения
    time_horizon: 64 # сколько опыта нужно собрать для каждого агента, прежде чем добавлять его в буфер
    summary_freq: 10000 # количество опыта, который необходимо собрать перед созданием и отображением статистики
```
Decision Requester - запрашивает решение через регулярные промежутки времени.

Behavior Parameters - определяет принятие объектом решений, в него указывается какой тип поведения будет использоваться: уже обученная модель или удалённый процесс обучения.

## Задание 3
###Доработать сцену и обучить ML-Agent таким образом, чтобы шар перемещался между двумя кубами разного цвета. Кубы должны, как и впервом задании, случайно изменять кооринаты на плоскости.
1. Добавим второй куб, создадим для него цвет
![2022-10-20_16-35-14](https://user-images.githubusercontent.com/86101819/196966748-444076bf-d6a3-49ef-ac59-43d5cd3e2edb.png)
2. Изменяем код C#, добавляем второй таргет
```cs
using System.Collections;
using System.Collections.Generic;
using UnityEngine;
using Unity.MLAgents;
using Unity.MLAgents.Sensors;
using Unity.MLAgents.Actuators;

public class RollerAgent : Agent
{
    Rigidbody rBody;
    // Start is called before the first frame update
    void Start()
    {
        rBody = GetComponent<Rigidbody>();
    }

    public GameObject Target1;
    public GameObject Target2;
    private bool target1Collected;
    private bool target2Collected;
    public override void OnEpisodeBegin()
    {
          if (this.transform.localPosition.y < 0)
    {
        this.rBody.angularVelocity = Vector3.zero;
        this.rBody.velocity = Vector3.zero;
        this.transform.localPosition = new Vector3(0, 0.5f, 0);
    }

    Target1.transform.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
    Target2.transform.localPosition = new Vector3(Random.value * 8-4, 0.5f, Random.value * 8-4);
    Target1.SetActive(true);
    Target2.SetActive(true);
    target1Collected = false;
    target2Collected = false;
    }
    public override void CollectObservations(VectorSensor sensor)
    {
         sensor.AddObservation(Target1.transform.localPosition);
    sensor.AddObservation(Target2.transform.localPosition);
    sensor.AddObservation(this.transform.localPosition);
    sensor.AddObservation(target1Collected);
    sensor.AddObservation(target2Collected);
    sensor.AddObservation(rBody.velocity.x);
    sensor.AddObservation(rBody.velocity.z);
    }
    public float forceMultiplier = 10;
    public override void OnActionReceived(ActionBuffers actionBuffers)
    {Vector3 controlSignal = Vector3.zero;
    controlSignal.x = actionBuffers.ContinuousActions[0];
    controlSignal.z = actionBuffers.ContinuousActions[1];
    rBody.AddForce(controlSignal * forceMultiplier);

    float distanceToTarget1 = Vector3.Distance(this.transform.localPosition, Target1.transform.localPosition);
    float distanceToTarget2 = Vector3.Distance(this.transform.localPosition, Target2.transform.localPosition);

    if (!target1Collected & distanceToTarget1 < 1.42f)
    {
        target1Collected = true;
        Target1.SetActive(false);
    }

    if (!target2Collected & distanceToTarget2 < 1.42f)
    {
        target2Collected = true;
        Target2.SetActive(false);
    }

    if(target1Collected & target2Collected)
    {
        SetReward(1.0f);
        EndEpisode();
    }
    else if (this.transform.localPosition.y < 0)
    {
        EndEpisode();
    }
}
}
```
3.Создаем несколько моделей и обучаем их
![2022-10-20_16-34-53](https://user-images.githubusercontent.com/86101819/196967173-9e02abf5-5c71-43bc-8afe-05cffe0c7a43.png)
4.Получаем корректную работу и обученную модель, которая работает с двумя кубами одновременно
![2022-10-20_16-46-38](https://user-images.githubusercontent.com/86101819/196967755-0646048c-48c3-4ab6-b6ac-a17c071d5810.png)

## Выводы
По итогу, я понял, и научился работать с MLagent-ом, разобрался в его структуре, способе применения, конфигурации. Понравилось работать с данной технологией.
Баланс в играх, как мне кажется, заключается в сложности и интересности игрового опыта, ибо баланс позволяет задавать правила игры и челенджи для игрока. Машинное обучение служит хорошим инструментом, чтобы задавать окружению или NPC тех качеств и способносей, которые смогут разнообразить опыт игрока, сделать его более увлекательным и живым, проработанным и способным составить конкуренцию игроку

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
