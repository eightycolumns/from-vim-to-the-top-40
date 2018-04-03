FROM debian:9

RUN apt-get update && apt-get -y install \
  csound=1:6.08.0~dfsg-1 \
  make=4.1-9.1 \
  samplerate-programs=0.1.8-8+b2

RUN useradd -m csound

USER csound
