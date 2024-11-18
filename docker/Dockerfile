FROM python:3.10-slim-bullseye
LABEL maintainer="mlops.study@gmail.com"

ARG APP_HOME=/home/hj
ARG RESOURCE_PATH=resources
ARG SOURCE_PATH=src

RUN groupadd --gid 1000 hj \
    && useradd --uid 1000 --gid hj --shell /bin/bash --create-home hj

COPY --chown=hj:hj ${RESOURCE_PATH}/ ${APP_HOME}/${RESOURCE_PATH}/
COPY --chown=hj:hj ${SOURCE_PATH}/ ${APP_HOME}/${SOURCE_PATH}/
COPY --chown=hj:hj ../app.py ${APP_HOME}/app.py
COPY --chown=hj:hj ../requirements.txt ${APP_HOME}/requirements.txt

RUN pip3 install --no-cache-dir \
         -r ${APP_HOME}/requirements.txt

USER hj

WORKDIR ${APP_HOME}

# EXPOSE functions as a type of documentation between the person who builds the image and the person
# who runs the container, about which ports are intended to be published.
EXPOSE 8000

ENTRYPOINT ["python", "app.py"]