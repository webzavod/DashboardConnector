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

