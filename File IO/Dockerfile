FROM ubuntu:trusty

RUN apt-get update
RUN apt-get install -y socat
RUN echo "Sample text" > abc.txt

CMD socat TCP4-LISTEN:9001,fork SYSTEM:'cat abc.txt'
