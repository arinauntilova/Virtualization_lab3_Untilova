# Задание 1.

Создайте образ Docker приложения и загрузите его на Docker Hub:

`docker build -t kubia .`

`docker run --name untilova_virt_lab_3 -p 8080:8080 -d kubia`

![image](https://github.com/arinauntilova/Virtualization_lab3_Untilova/assets/43550219/e0e59df4-3e12-414c-844d-0535611f578c)

`docker tag kubia ariannauntilova/kubia`

`docker login`

`docker push ariannauntilova/kubia`

![image](https://github.com/arinauntilova/Virtualization_lab3_Untilova/assets/43550219/9f08ca19-023e-4544-a268-c54c1cf31ded)

Запуск кластера: 

`minikube start`

![image](https://github.com/arinauntilova/Virtualization_lab3_Untilova/assets/43550219/ec6722dd-cc70-4e11-82fc-6f702b8cf2be)

Разворчаиваем приложением с именем kubia:

`kubectl create deployment kubia --image=ariannauntilova/kubia`

![image](https://github.com/arinauntilova/Virtualization_lab3_Untilova/assets/43550219/2ff7ae51-28d0-419a-8e90-79b0adf667e0)

Развернем приложение с индексом репликации = 3 на кластере Kubernetes. Тип службы – LoadBalancer:

Создав службу типа LoadBalancer, создаем внешний балансировщик нагрузки, и доступ к модулям будет осуществляться через общедоступный IP-адрес балансировщика нагрузки:

`kubectl expose deployment kubia --type=LoadBalancer --port=8080`

Выводим все сервисы в пространстве имён

`kubectl get services`

![image](https://github.com/arinauntilova/Virtualization_lab3_Untilova/assets/43550219/6e36ef07-43a5-4f3d-8eeb-5cddd2554b26)

Масштабирование набора реплик:

`kubectl scale deployment kubia --replicas=3`

![image](https://github.com/arinauntilova/Virtualization_lab3_Untilova/assets/43550219/02e7781c-6013-4378-aafe-d02a40bffee0)


`kubectl get deployments`

Выводим все поды в пространстве имён с подробным описанием:

`kubectl get pods -o wide`

![image](https://github.com/arinauntilova/Virtualization_lab3_Untilova/assets/43550219/68f702c7-5aeb-44ae-bac0-a581e5e0f3ae)

Обратитесь несколько раз к приложению с помощью утилиты curl:

Запросы, отправленные в службу, будут отправлены во все три модуля

Служба выбирает один из трех адресов подов в качестве пункта назначения

`curl -s 10.103.217.134:8080`

![image](https://github.com/arinauntilova/Virtualization_lab3_Untilova/assets/43550219/d4c87211-043c-44b3-834b-e6282b0fec74)



# Задание 2. Попробуйте запустить в кластере Kubernetes одно из Ваших приложений из тем «Docker» или «Docker-compose».

Использую образ ariannauntilova/attm2 из Docker Hub (лр_1):

Разворчаиваем приложением с именем kubiapart2:

`kubectl create deployment kubiapart2 --image=ariannauntilova/attm2:latest`

Создаем службу типа LoadBalancer:

`kubectl expose deployment/kubiapart2 --type="LoadBalancer" --port=80`

![image](https://github.com/arinauntilova/Virtualization_lab3_Untilova/assets/43550219/50767f6c-099e-44fc-85a1-7bac1706d175)

`kubectl get services`

![image](https://github.com/arinauntilova/Virtualization_lab3_Untilova/assets/43550219/df1534ed-fa39-4ad0-b1e4-7b3af0b87b41)

`kubectl get pods -o wide`

![image](https://github.com/arinauntilova/Virtualization_lab3_Untilova/assets/43550219/e75ade52-6109-4464-9cbf-9eef0231624d)

`curl 10.244.0.39:80`

![image](https://github.com/arinauntilova/Virtualization_lab3_Untilova/assets/43550219/165c8feb-a12a-4420-a817-8fe4eb08fd71)
