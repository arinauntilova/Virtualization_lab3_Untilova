#Задание 1.

Создайте образ Docker приложения и загрузите его на Docker Hub:

docker build -t kubia_lab3 .

docker run --name unt_virt_lab_3 -p 80:80 -d kubia_lab3

docker login

docker push ariannauntilova/kubia_lab3

minikube start

kubectl create deployment kubialab3 --image=ariannauntilova/kubia_lab3

kubectl get deployments

kubectl expose deployment kubialab3 --type=LoadBalancer --port=8080

kubectl get services

kubectl get pods

kubectl scale deployment kubialab3 --replicas=3

kubectl get pods -o wide



2.  Разверните приложение с индексом репликации = 3 на кластере Kubernetes. Тип службы – LoadBalancer.
3.  Обратитесь несколько раз к приложению с помощью утилиты curl. Сделайте вывод.  

#Задание 2. Попробуйте запустить в кластере Kubernetes одно из Ваших приложений из тем «Docker» или «Docker-compose».
