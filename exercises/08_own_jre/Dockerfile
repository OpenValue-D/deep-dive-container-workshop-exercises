FROM azul/zulu-openjdk:21.0.5-jdk AS java

RUN apt-get update \
   && DEBIAN_FRONTEND=noninteractive apt-get install -y binutils
WORKDIR /app

RUN jlink \
    --add-modules ADD_MODULES_HERE \
    --compress zip-9 \
    --strip-debug \
    --no-header-files \
    --no-man-pages \
    --output /myjre

FROM my-distro

ENV JAVA_HOME=/opt/java
ENV PATH=$JAVA_HOME/bin:$PATH
COPY --from=java /myjre /opt/java
ENTRYPOINT ["java"]
