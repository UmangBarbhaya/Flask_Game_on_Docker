FROM umangbarbhaya/ubuntuflask:v1
COPY . /app
WORKDIR /app
RUN python3 -m venv venv
RUN /bin/bash -c "source venv/bin/activate"
ENTRYPOINT [ "python3" ]
CMD [ "main.py" ]