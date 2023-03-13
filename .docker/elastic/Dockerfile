#FROM elasticsearch:7.11.0
FROM elasticsearch:7.17.9

RUN /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-phonetic && \
    /usr/share/elasticsearch/bin/elasticsearch-plugin install analysis-icu