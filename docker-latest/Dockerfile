FROM docker:latest

COPY my_ca.crt /tmp/
RUN cat /tmp/my_ca.crt >>/etc/ssl/certs/ca-certificates.crt && rm /tmp/my_ca.crt

ENTRYPOINT ["docker-entrypoint.sh"]
CMD ["sh"]