FROM docker:dind

COPY my_ca.crt /tmp/
RUN cat /tmp/my_ca.crt >>/etc/ssl/certs/ca-certificates.crt && rm /tmp/my_ca.crt

VOLUME /var/lib/docker
EXPOSE 2375

ENTRYPOINT ["dockerd-entrypoint.sh"]
CMD []
