# WebMap
# -
# Cloned from: https://github.com/Hamza-Megahed/WebMap
# Original: Rev3rse Security: https://www.youtube.com/rev3rsesecurity
# Modified: 
#
# http://localhost:8000

FROM ubuntu:18.04

ENV DEBIAN_FRONTEND noninteractive

RUN apt-get update && apt-get install -y --allow-downgrades --allow-remove-essential --allow-change-held-packages \
    python3 python3-pip curl wget git wkhtmltopdf libssl1.0-dev nmap tzdata

RUN mkdir /opt/xml && mkdir /opt/notes && \
    wget -P /opt/ https://github.com/jpradoar/webmap/raw/master/docker/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz && \
    cd /opt/ && tar -xvf /opt/wkhtmltox-0.12.4_linux-generic-amd64.tar.xz

RUN pip3 install Django requests xmltodict && \
    cd /opt/ && django-admin startproject nmapdashboard && cd /opt/nmapdashboard && \
    git clone https://github.com/Hamza-Megahed/WebMap.git nmapreport && \
    cd nmapreport && git checkout v2.3/master

COPY settings.py /opt/nmapdashboard/nmapdashboard/
COPY urls.py /opt/nmapdashboard/nmapdashboard/
# COPY vimrc /root/.vimrc
COPY tzdata.sh /root/tzdata.sh
COPY startup.sh /startup.sh

RUN cd /opt/nmapdashboard && python3 manage.py migrate
RUN apt-get autoremove -y
RUN ln -s /opt/nmapdashboard/nmapreport/token.py /root/token

EXPOSE 8000

ENTRYPOINT ["bash", "/startup.sh"]
