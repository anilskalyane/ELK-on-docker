ARG ELK_VERSION

FROM docker.elastic.co/beats/metricbeat:${ELK_VERSION}

# Switch to root user to perform system-wide updates
USER root

# Update package list and install ca-certificates
RUN apt-get update \
    && apt-get install -y ca-certificates \
    && apt-get clean

# Enable CA certificate trust
RUN update-ca-certificates

# Switch to metricbeat user
USER metricbeat

# Example CMD for metricbeat setup
CMD update-ca-certificates && \
    metricbeat setup -e --index-management --dashboards \
    -E "output.logstash.enabled=false" \
    -E "output.elasticsearch.hosts=['https://elasticsearch:9200']" \
    -E "output.elasticsearch.ssl.certificate_authorities=['/etc/ssl/certs/ca-certificates.crt']" \
    -E "output.elasticsearch.ssl.certificates=${CONFIG_DIR}/metricbeat.crt" \
    -E "output.elasticsearch.ssl.key=${CONFIG_DIR}/metricbeat.key"

#USER root
#RUN yum-config-manager --save --setopt=base.skip_if_unavailable=true
#RUN yum install ca-certificates -y
#RUN update-ca-trust force-enable

#USER metricbeat
#CMD  update-ca-trust extract \
#    metricbeat setup -e --index-management --dashboards -E "output.logstash.enabled=false" -E "output.elasticsearch.hosts=['https://elasticsearch:9200']" -E "output.elasticsearch.ssl.certificate_authorities=["/etc/pki/ca-trust/source/anchors/ca.crt"]" -E "output.elasticsearch.ssl.certificates=${CONFIG_DIR}/metricbeat.crt" -E "output.elasticsearch.ssl.key=${CONFIG_DIR}/metricbeat.key"
