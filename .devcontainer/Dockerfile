ARG AIRFLOW_BASE_IMAGE=apache/airflow:2.5.0-python3.8

FROM ${AIRFLOW_BASE_IMAGE}

ENV DIVID_DIR=/home/divid

COPY ./port/requirements.txt ${DIVID_DIR}/port_requirements.txt
COPY ./port_ml/requirements_tiny.txt ${DIVID_DIR}/port_ml_requirements.txt

RUN pip install -U pip
RUN pip install --no-cache-dir -r ${DIVID_DIR}/port_requirements.txt
RUN pip install --no-cache-dir -r ${DIVID_DIR}/port_ml_requirements.txt

# install reqs
# re-install because there is a conflict between requiements
RUN pip install apache-airflow==2.3.0

WORKDIR ${DIVID_DIR}
# COPY ./wait_for_connection.sh .
COPY ./port_ml ./port_ml
COPY ./port/port ./port
COPY ./divid_api ./divid_api

#ARG AIRFLOW_GID=10240
USER root
#RUN addgroup --gid 10240 host_group
#RUN usermod -a -G 10240 airflow
#USER airflow

ENV PYTHONPATH=/home/airflow/.local/lib/python3.8/site-packages:${DIVID_DIR}:${DIVID_DIR}/divid_api
