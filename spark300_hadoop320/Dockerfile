## A Dockerfile which includes S3 dependencies
ARG BASE_IMG="gcr.io/spark-operator/spark:v3.0.0-hadoop3"
FROM $BASE_IMG
WORKDIR /

# Reset to root to run installation tasks
USER 0

# Get Curl
RUN apt-get update --allow-releaseinfo-change && apt-get install -y curl && \
    rm -rf /var/cache/apt/*

# Get the dependencies
ARG POSTGRESQL_VERSION="42.2.23"
ARG AWS_SDK_VERSION="1.11.375"
ARG AWS_HADOOP_VERSION="3.2.0"
ARG SQL_SERVER_VERSION="8.4.1.jre8"
ARG DELTA_VERSION="0.8.0"
ARG SPARK_XML_VERSION="0.14.0"
ARG HAPI_FHIR_VERSION="5.1.0"

RUN curl https://repo1.maven.org/maven2/io/delta/delta-core_2.12/${DELTA_VERSION}/delta-core_2.12-${DELTA_VERSION}.jar -o /opt/spark/jars/delta-core_2.12-${DELTA_VERSION}.jar
RUN curl https://repo1.maven.org/maven2/com/microsoft/sqlserver/mssql-jdbc/${SQL_SERVER_VERSION}/mssql-jdbc-${SQL_SERVER_VERSION}.jar -o /opt/spark/jars/mssql-jdbc-${SQL_SERVER_VERSION}.jar
RUN curl https://jdbc.postgresql.org/download/postgresql-${POSTGRESQL_VERSION}.jar -o /opt/spark/jars/postgresql-${POSTGRESQL_VERSION}.jar
RUN curl https://repo1.maven.org/maven2/com/amazonaws/aws-java-sdk-bundle/${AWS_SDK_VERSION}/aws-java-sdk-bundle-${AWS_SDK_VERSION}.jar -o /opt/spark/jars/aws-java-sdk-bundle-${AWS_SDK_VERSION}.jar
RUN curl https://repo1.maven.org/maven2/org/apache/hadoop/hadoop-aws/${AWS_HADOOP_VERSION}/hadoop-aws-${AWS_HADOOP_VERSION}.jar -o /opt/spark/jars/hadoop-aws-${AWS_HADOOP_VERSION}.jar
RUN curl https://repo1.maven.org/maven2/com/databricks/spark-xml_2.12/${SPARK_XML_VERSION}/spark-xml_2.12-${SPARK_XML_VERSION}.jar -o /opt/spark/jars/spark-xml_2.12-${SPARK_XML_VERSION}.jar
RUN curl https://repo1.maven.org/maven2/ca/uhn/hapi/fhir/hapi-fhir-structures-r4/${HAPI_FHIR_VERSION}/hapi-fhir-structures-r4-${HAPI_FHIR_VERSION}.jar -o /opt/spark/jars/hapi-fhir-structures-r4-${HAPI_FHIR_VERSION}.jar

WORKDIR /opt/spark/work-dir
ENTRYPOINT [ "/opt/entrypoint.sh" ]

# Specify the User that the actual main process will run as
ARG SPARK_UID=185
USER ${SPARK_UID}