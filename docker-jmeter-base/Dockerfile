FROM alpine:3.15

ENV JMETER_VERSION "5.4.3"
ENV JMETER_HOME /opt/jmeter
ENV JMETER_BIN ${JMETER_HOME}/bin
ENV PATH ${JMETER_BIN}:$PATH
ARG TZ='Asia/Shanghai'
ENV DEFAULT_TZ ${TZ}
LABEL maintainer="yangkuankuanchn@gmail.com"

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk -U upgrade \
    && apk add --no-cache curl openjdk8-jre bash tzdata \
    && apk add --no-cache --upgrade grep \
    && cp /usr/share/zoneinfo/${DEFAULT_TZ} /etc/localtime \
    && apk del tzdata \
    && rm -rf /var/cache/apk/*

# 下载安装 jmeter
RUN curl -L https://dlcdn.apache.org//jmeter/binaries/apache-jmeter-${JMETER_VERSION}.tgz > /tmp/jmeter.tgz \
    && tar -xvf /tmp/jmeter.tgz -C /opt \
    && mv /opt/apache-jmeter-${JMETER_VERSION} ${JMETER_HOME} \
    && rm /tmp/jmeter.tgz \
    # 安装插件管理器及相关命令行脚本
    && curl -s -L https://jmeter-plugins.org/get/ > ${JMETER_HOME}/lib/ext/jmeter-plugins-manager.jar \
    && java -cp ${JMETER_HOME}/lib/ext/jmeter-plugins-manager.jar org.jmeterplugins.repository.PluginManagerCMDInstaller \
    && CMDRUNNER_VERSION=`grep -Po '(?<=cmdrunner-)\d.\d' ${JMETER_HOME}/bin/PluginsManagerCMD.sh` \
    && curl -s -L http://search.maven.org/remotecontent?filepath=kg/apc/cmdrunner/${CMDRUNNER_VERSION}/cmdrunner-${CMDRUNNER_VERSION}.jar > ${JMETER_HOME}/lib/cmdrunner-${CMDRUNNER_VERSION}.jar \
    && cd ${JMETER_HOME} \
    && rm -rf README.md printable_docs NOTICE licenses LICENSE extras docs

CMD ["/bin/bash"]