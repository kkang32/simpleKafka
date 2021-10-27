## kafka 맛보기

- 설치파일 다운로드

    - https://kafka.apache.org/downloads

- 압축 해제후 zookeeper실행 (kafka는 zookeeper위에서 동작함)

    ```
    bin/zookeeper-server-start.sh config/zookeeper.properties
    ```

- kafka실행

    ```
    bin/kafka-server-start.sh config/server.properties
    ```

- 토픽 생성

    ``` 
    bin/kafka-topics.sh --create --topic quickstart-events --bootstrap-server localhost:9092 --partitions 1 --replication-factor 1
    ```

- 토픽 확인

    ```
    bin/kafka-topics.sh --list --bootstrap-server localhost:9092
    ```

- 토픽 설정 확인

    ```
    bin/kafka-topics.sh --describe --topic quickstart-events --bootstrap-server localhost:9092
    ```

- producer, consumer생성

    - 콘솔1(producer)

      ```
      bin/kafka-console-producer.sh --topic quickstart-events --bootstrap-server localhost:9092
      ```

    - 콘솔2(consumer)

      ```
      bin/kafka-console-consumer.sh --topic quickstart-events --from-beginning --bootstrap-server localhost:9092
      ```

    - 콘솔 1에서 메시지를 입력하면 콘솔 2에서 받아오는걸 확인할 수 있음
 
## Spring boot에 붙이기

- 빌드 후 java -jar [파일명.jar] 로 실행한다.

- 아래와 같이 요청하면 

```
curl -XPOST 'http://localhost:8082/test/publish' -H 'Content-Type:application/json' -d '{"msg":"hello world!"}'
```

- producer에서 레코드를 생성하면

```
2021-10-27 10:31:34.225  INFO 6768 --- [ad | producer-1] c.example.kafka.producer.CustomProducer  : publish message: hello world!
```

- cosumer에서 처리함

```
2021-10-27 10:31:34.225  INFO 6768 --- [ntainer#0-0-C-1] c.example.kafka.consumer.CustomConsumer  : CONSUME PAYLOAD : hello world!
```
