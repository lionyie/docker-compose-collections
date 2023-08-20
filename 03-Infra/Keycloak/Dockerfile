FROM quay.io/keycloak/keycloak:21.1.1
USER root
RUN microdnf update -y && microdnf install -y glibc-langpack-en gzip hostname java-11-openjdk-headless openssl tar which && microdnf clean all
USER 1000
EXPOSE 8080
