# ter-homework01
# Домашнее задание к занятию «Введение в Terraform»

### Цели задания

1. Установить и настроить Terrafrom.
2. Научиться использовать готовый код.

------

### Чек-лист готовности к домашнему заданию

1. Скачайте и установите **Terraform** версии =1.5.Х (версия 1.6 может вызывать проблемы с Яндекс провайдером) . Приложите скриншот вывода команды ```terraform --version```. ![изображение](https://github.com/Razbor/ter-homework01/assets/19568831/47c975cf-f949-4f56-91a2-c88c463862b9)

2. Скачайте на свой ПК этот git-репозиторий. Исходный код для выполнения задания расположен в директории **01/src**.![изображение](https://github.com/Razbor/ter-homework01/assets/19568831/29726ba0-83c8-4c9f-b152-fac9e07147bc)

3. Убедитесь, что в вашей ОС установлен docker.![изображение](https://github.com/Razbor/ter-homework01/assets/19568831/b163bdc3-0ec9-44ab-8e9b-99e58f56c038)

4. Зарегистрируйте аккаунт на сайте https://hub.docker.com/, выполните команду docker login и введите логин, пароль.![изображение](https://github.com/Razbor/ter-homework01/assets/19568831/c96c0496-f2b6-4223-b9c7-9aa8b19eeb16)


------


------

### Задание 1

1. Перейдите в каталог [**src**](https://github.com/netology-code/ter-homeworks/tree/main/01/src). Скачайте все необходимые зависимости, использованные в проекте. 
2. Изучите файл **.gitignore**. В каком terraform-файле, согласно этому .gitignore, допустимо сохранить личную, секретную информацию?
#### Ответ: Личная информация сохраняется в personal.auto.tfvars
3. Выполните код проекта. Найдите  в state-файле секретное содержимое созданного ресурса **random_password**, пришлите в качестве ответа конкретный ключ и его значение.
![изображение](https://github.com/Razbor/ter-homework01/assets/19568831/03dcc194-f730-4e1c-a7af-16ca80d88d2d)

4. Раскомментируйте блок кода, примерно расположенный на строчках 29–42 файла **main.tf**.
Выполните команду ```terraform validate```. Объясните, в чём заключаются намеренно допущенные ошибки. Исправьте их.
##### Ответ:   
    Исправлено имя "nginx"`` в resource "docker_image"`
    Исправлен идентификатор random_password.random_string_FAKE.resulT на random_password.random_string.result
    Исправлено имя "docker_container" "1nginx" убрал цифру из имени.

5. Выполните код. В качестве ответа приложите: исправленный фрагмент кода и вывод команды ```docker ps```.
```
resource "docker_image" "nginx" {
  name         = "nginx:latest"
  keep_locally = true
}

resource "docker_container" "nginx" {
  image = docker_image.nginx.image_id
  name  = "example_${random_password.random_string.result}"

  ports {
    internal = 80
    external = 8000
  }
}
```
![изображение](https://github.com/Razbor/ter-homework01/assets/19568831/c4b04cbe-7356-48b6-8955-c6a6be4833e5)

6. Замените имя docker-контейнера в блоке кода на ```hello_world```. Не перепутайте имя контейнера и имя образа. Мы всё ещё продолжаем использовать name = "nginx:latest". Выполните команду ```terraform apply -auto-approve```.
Объясните своими словами, в чём может быть опасность применения ключа  ```-auto-approve```. Догадайтесь или нагуглите зачем может пригодиться данный ключ? В качестве ответа дополнительно приложите вывод команды ```docker ps```.
![изображение](https://github.com/Razbor/ter-homework01/assets/19568831/fb5fde8b-7dd8-422f-93c3-82161798c7eb)
7. Уничтожьте созданные ресурсы с помощью **terraform**. Убедитесь, что все ресурсы удалены. Приложите содержимое файла **terraform.tfstate**.
![изображение](https://github.com/Razbor/ter-homework01/assets/19568831/2ba8e629-c42e-469f-9f97-7e4ba38919a3)

8. Объясните, почему при этом не был удалён docker-образ **nginx:latest**. Ответ **ОБЯЗАТЕЛЬНО НАЙДИТЕ В ПРЕДОСТАВЛЕННОМ КОДЕ**, а затем **ОБЯЗАТЕЛЬНО ПОДКРЕПИТЕ** строчкой из документации [**terraform провайдера docker**](https://docs.comcloud.xyz/providers/kreuzwerker/docker/latest/docs).  (ищите в классификаторе resource docker_image )


------


