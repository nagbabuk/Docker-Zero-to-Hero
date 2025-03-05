#####################
# Base image
#####################

FROM ubuntu AS build
RUN apt-get update && apt-get install -y python3 python3-pip python3-venv

WORKDIR /app

RUN python3 -m venv venv1 && \
    source venv1/bin/activate && \
    pip install --no-cache-dir -r requirements.txt

################################################
# Here starts the magic of multi stage build
################################################
FROM scratch

COPY --from=build requirements.txt /app
COPY --from=build devops /app/

EXPOSE 8080
CMD source venv1/bin/activate && python3 manage.py runserver 0.0.0.0:8000