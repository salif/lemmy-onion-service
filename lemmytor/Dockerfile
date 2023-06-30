FROM alpine:latest
RUN apk --no-cache add tor
COPY torrc /etc/tor/torrc
RUN chown -R tor /etc/tor
RUN mkdir /var/lib/tor/hidden_lemmy_service/ 
RUN chown -R tor /var/lib/tor/hidden_lemmy_service/
RUN chmod 700 /var/lib/tor/hidden_lemmy_service/
USER tor
ENTRYPOINT ["tor"]
CMD ["-f", "/etc/tor/torrc"]
