FROM confluentinc/cp-kafka-connect:5.3.1

RUN confluent-hub install \
    --worker-configs /etc/kafka/connect-distributed.properties \
    --no-prompt \
    --component-dir /usr/share/java \
    -- confluentinc/kafka-connect-datagen:latest

