University: [ITMO University](https://itmo.ru/ru/) <br>
Faculty: [FICT](https://fict.itmo.ru) <br>
Course: [Introduction to distributed technologies](https://github.com/itmo-ict-faculty/introduction-to-distributed-technologies) <br>
Year: 2024/2025 <br>
Group: K4111c <br>
Author: Sadikov Maksim Andreevich <br>
Lab: [Лабораторная работа №1 "Установка Docker и Minikube, мой первый манифест."](https://itmo-ict-faculty.github.io/introduction-to-distributed-technologies/education/labs2023_2024/lab1/lab1/) <br>
Date of create: 14.11.2024 <br>
Date of finished: <br>

### Ход работы

Были установлены компоненты для выполнения лабораторной работы на Windows 11: **minikube**, **Docker**

```
docker version
```

![alt text](screenshots/image.png)

```
minikube version
```

![alt text](screenshots/image-1.png)

Для запуска кластера minikube была выполнена команда:

```
minikube start
```

Был написан манифест для образа HashiCorp Vault `vault-pod.yaml`

```
kind: Pod
apiVersion: v1
metadata:
  name: vault
  labels:
    app: vault
spec:
  containers:
    - name: vault-container
      image: hashicorp/vault:latest

```

После этого к кластеру был применен манифест командой и создан под командой:

```
kubectl apply -f vault-pod.yaml
```

![alt text](screenshots/image-3.png)
![alt text](screenshots/image-2.png)

После этого был создан сервис для доступа к контейнеру

```
minikube kubectl -- expose pod vault --type=NodePort --port=8200
```

![alt text](screenshots/image-4.png)

И далее был настроен проброс порта для доступа на хосте

```
minikube kubectl -- port-forward service/vault 8200:8200
```

![alt text](screenshots/image-5.png)

Для авторизации был использован токен из логов пода `minikube kubectl -- logs vault`

![alt text](screenshots/image-8.png)
![alt text](screenshots/image-7.png)
![alt text](screenshots/image-6.png)

### Диаграмма контейнеров и сервисов

![alt text](screenshots/vault-pod-diagram.drawio.png)
