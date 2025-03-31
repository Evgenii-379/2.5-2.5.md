# **Домашнее задание к занятию «Helm»**-***Вуколов Евгений***
 
### Цель задания
 
В тестовой среде Kubernetes необходимо установить и обновить приложения с помощью Helm.
 
------
 
### Чеклист готовности к домашнему заданию
 
1. Установленное k8s-решение, например, MicroK8S.
2. Установленный локальный kubectl.
3. Установленный локальный Helm.
4. Редактор YAML-файлов с подключенным репозиторием GitHub.
 
------
 
### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания
 
1. [Инструкция](https://helm.sh/docs/intro/install/) по установке Helm. [Helm completion](https://helm.sh/docs/helm/helm_completion/).
 
------
 
### Задание 1. Подготовить Helm-чарт для приложения
 
1. Необходимо упаковать приложение в чарт для деплоя в разные окружения. 
2. Каждый компонент приложения деплоится отдельным deployment’ом или statefulset’ом.
3. В переменных чарта измените образ приложения для изменения версии.
 
------
### Задание 2. Запустить две версии в разных неймспейсах
 
1. Подготовив чарт, необходимо его проверить. Запуститe несколько копий приложения.
2. Одну версию в namespace=app1, вторую версию в том же неймспейсе, третью версию в namespace=app2.
3. Продемонстрируйте результат.
 
### Правила приёма работы
 
1. Домашняя работа оформляется в своём Git репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд `kubectl`, `helm`, а также скриншоты результатов.
3. Репозиторий должен содержать тексты манифестов или ссылки на них в файле README.md.


# **Решение**

## **Задание 1**

- Установил менеджер пакетов для microk8s Helm:

- ![scrin](https://github.com/Evgenii-379/2.5-2.5.md/blob/main/Снимок%20экрана%202025-03-31%20152534.png)

- Подготовил Helm-чарт для приложения Nginx. Этот Helm-чарт создаётся для развёртывания Nginx в Kubernetes-кластере с дополнительными компонентами:

```
1. Chart.yaml:
- Метаданные чарта (имя, описание, версии)

- Определяет тип приложения и версии

2. values.yaml:
- replicaCount: количество реплик Nginx

- image: настройки образа Nginx

- service: конфигурация сервиса

3. deployment.yaml:
- Создаёт поды с Nginx

- Использует образ из переменных .Values.image

- Открывает 80 порт 

4. logs-deployment.yaml:
- Отдельный под с busybox

- Выводит логи каждые 10 секунд

5. service.yaml:
- Создаёт ClusterIP сервис для доступа к Nginx

- Порт берётся из .Values.service.port
```
- ![scrin](https://github.com/Evgenii-379/2.5-2.5.md/blob/main/Снимок%20экрана%202025-03-31%20215941.png)


## **Задание 2**

- Развёртывание разных версий в разных namespace:
Создаю namespace app1 и app2:

- ![scrin](https://github.com/Evgenii-379/2.5-2.5.md/blob/main/Снимок%20экрана%202025-03-31%20200238.png)

- Затем разворачиваю  Helm-чарты:

- ![scrin](https://github.com/Evgenii-379/2.5-2.5.md/blob/main/Снимок%20экрана%202025-03-31%20220416.png)

- Проверяю запущенные версии:
 
- ![scrin](https://github.com/Evgenii-379/2.5-2.5.md/blob/main/Снимок%20экрана%202025-03-31%20220813.png)

- Результат в dashboard microk8s : 
- ![scrin](https://github.com/Evgenii-379/2.5-2.5.md/blob/main/Снимок%20экрана%202025-03-31%20220959.png)
- ![scrin](https://github.com/Evgenii-379/2.5-2.5.md/blob/main/Снимок%20экрана%202025-03-31%20221013.png)

- Ссылки на манифесты: 

[deployment.yaml](https://github.com/Evgenii-379/2.5-2.5.md/blob/main/nginx-chart/templates/deployment.yaml)

[logs-deployment.yaml](https://github.com/Evgenii-379/2.5-2.5.md/blob/main/nginx-chart/templates/logs-deployment.yaml)

[service.yaml](https://github.com/Evgenii-379/2.5-2.5.md/blob/main/nginx-chart/templates/service.yaml)

[Chart.yaml](https://github.com/Evgenii-379/2.5-2.5.md/blob/main/nginx-chart/Chart.yaml)

[values.yaml](https://github.com/Evgenii-379/2.5-2.5.md/blob/main/nginx-chart/values.yaml)












