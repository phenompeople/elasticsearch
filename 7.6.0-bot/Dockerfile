FROM phenompeople/oraclejre:latest
LABEL maintainer="bharath.muthineni@phenompeople.com" \
	  version="7.6.0" \
	  project="elasticsearch"
EXPOSE 9200 9300
ARG ELASTIC_VERSION=7.6.0
ARG ES_HOME=/usr/local/elasticsearch
RUN yum install which -q -y && \
	groupadd -g 403 elasticsearch && \
	useradd -u 403 -g 403 elasticsearch && \
	wget -q -O /tmp/elasticsearch.tar.gz https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-${ELASTIC_VERSION}-linux-x86_64.tar.gz && \
	tar -xzf /tmp/elasticsearch.tar.gz -C /usr/local && \
	chown -R elasticsearch:elasticsearch /usr/local/elasticsearch-${ELASTIC_VERSION} && \
	sed -e '/-Xmx2g/d' -e  '/-Xms2g/d' -i /usr/local/elasticsearch-${ELASTIC_VERSION}/config/jvm.options && \
	ln -sf /usr/local/elasticsearch-${ELASTIC_VERSION} ${ES_HOME} && \
	rm -rf /tmp/elasticsearch.tar.gz
ENV JAVA_HOME=/usr/local/jre
RUN /usr/local/elasticsearch/bin/elasticsearch-plugin install analysis-icu
RUN /usr/local/elasticsearch/bin/elasticsearch-plugin install analysis-phonetic
RUN /usr/local/elasticsearch/bin/elasticsearch-plugin install --batch repository-s3
USER elasticsearch
ENV ES_HOME=${ES_HOME}
ENTRYPOINT ["/usr/local/elasticsearch/bin/elasticsearch"]
