# Установка с использованием контейнеров Docker

## Получение контейнеров

Образ контейнера находится в файле  webzavod_datalens-1c-connector-XXX.tar. 

Для импорта контейнера необходимо перейти в папку, куда скачан файл и выполнить команду в консоли:

Для Linux 

```sh
docker image load -i ./webzavod_datalens-1c-connector-XXX.tar
```

Для Windows 

```powershell
docker image load -i webzavod_datalens-1c-connector-XXX.tar
```

## Установка и запуск контейнеров

Установка и запуск контейнеров может быть выполнена с использованием yml файла. При этом в отдельный контейнер устанавливается Apache CouchDB, официальный образ которого скачивается из репозитория Docker. YML  можно забрать из GitHub.

В Линукс

```shell
docker-compose start -f ./docker-compose-1c-datalens.yml
```

В Windows

```powershell
docker-compose start -f docker-compose-1c-datalens.yml
```

Для изменения порта по умолчанию (8080) нужно предварительно изменить секцию ports конейнера webzavod.datalens.1cconnector

```yaml
version: '3.4'
services:
 webzavod.datalens.1cconnector:
  image: webzavod/datalens-1c-connector
  ports:
   -"8080:80"
  links:
   -couchdb:couchdb
  deploy:
   replicas: 1 
 couchdb:
  image: couchdb
  ports:
   -"5984:5984"
  deploy:
   replicas: 1
```

## Проверка установки

Правильность установки можно проверить, последовательно запустив две команды в Linux:

```shell
curl http://<hostname>:5884
curl http://<hostname>:8080
```

При этом <hostname> заменяется на имя машины, на которой запущен Docker или localhost, если проверка осуществляется локально.

В Windows, по умолчанию, команды curl нет, поэтому проверка осуществляется в интернет-браузере, последовательно переходя по двум ссылкам:
http://<hostname>:5884/_utils, при этом будет показано окно, похожее на скриншот:
![image-20191205113220891](https://github.com/webzavod/1CDataLens/blob/master/Docs/images/image-20191205113220891.png)

http://<hostname>:8080/, при этом должно открыться окно 1С коннектора
![image-20191205113432980](https://github.com/webzavod/1CDataLens/blob/master/Docs/images/image-20191205113432980.png)

