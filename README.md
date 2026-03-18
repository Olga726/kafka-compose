# загрузить проект 
git clone https://github.com/Olga726/kafka-compose 
# запустить докер контейнеры  
docker-compose up -d 

# В localhost:8080 будет kowl, где удобно смотреть все про kafka
# На localhost:9092 будет сама кафка

# войти в консоль контейнера – 
docker exec -it kafka-compose-kafka-1 bash   
# name (docker ps) kafka-compose-kafka-1

# В Confluent Platform бинарники лежат в /usr/bin или /usr/bin/kafka
# создать топик Test
/usr/bin/kafka-topics --create --bootstrap-server localhost:9092 --replication-factor 1 --partitions 1 --topic Test

# список топиков
/usr/bin/kafka-topics --list --bootstrap-server localhost:9092

# удалить топик
/usr/bin/kafka-topics --delete --bootstrap-server localhost:9092 --topic Test

# отправить сообщение брокеру 
echo "Hello everyone" | /usr/bin/kafka-console-producer --broker-list localhost:9092 --topic Test
# --broker-list localhost:9092 — внутренний порт Kafka внутри контейнера (localhost в контейнере = сам контейнер Kafka).
# --topic Test — имя топика.

# Консумер для проверки (выведет все сообщения --from-beginning)
/usr/bin/kafka-console-consumer --bootstrap-server localhost:9092 --topic Test --from-beginning


