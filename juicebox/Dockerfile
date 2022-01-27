FROM gcr.io/ris-registry-shared/novnc:ubuntu20.04

RUN apt update && \
  apt install -y \
    default-jdk \
    libnss-sss \
    vim \
  && apt clean

WORKDIR /app/juicebox
RUN wget https://github.com/aidenlab/Juicebox/releases/download/v.2.13.07/juicebox.jar
WORKDIR /app/juicebox/scripts
COPY ./juicebox ./
RUN chmod 777 juicebox

ENV PASSWORD=hic
ENV PATH=/app/juicebox/scripts:$PATH
ENV TZ=America/Chicago
ENV LANG=C
