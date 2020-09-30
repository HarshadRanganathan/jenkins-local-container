FROM docker.io/sonatype/nexus3:3.25.1

# https://github.com/sonatype/docker-nexus3/blob/master/Dockerfile

WORKDIR ${NEXUS_HOME}

COPY orientdb.txt "${NEXUS_HOME}"
COPY start-nexus-repository-manager.sh "${SONATYPE_DIR}/start-nexus-repository-manager.sh"

EXPOSE 8081
USER nexus

ENV INSTALL4J_ADD_VM_PARAMS="-Xms1200m -Xmx1200m -XX:MaxDirectMemorySize=2g -Djava.util.prefs.userRoot=${NEXUS_DATA}/javaprefs"

CMD ["sh", "-c", "${SONATYPE_DIR}/start-nexus-repository-manager.sh"]
