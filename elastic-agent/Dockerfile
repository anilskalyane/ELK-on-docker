FROM ubuntu:20.04

RUN apt-get update && \
    apt-get -y install sudo python3-pip python3 && \
    apt-cache search python3-pip && \
    apt-get clean && rm -rf /var/lib/apt/lists/*

RUN pip3 install requests PyYaml elastic-agent-setup==0.0.11

ADD install.py /install.py
RUN chmod +x /install.py

CMD ["/install.py"]
ENTRYPOINT ["python3"]

