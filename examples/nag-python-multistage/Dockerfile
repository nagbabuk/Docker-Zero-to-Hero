#####################
# Base image
#####################

FROM ubuntu AS build
RUN apt-get update && apt-get install -y python3 python3-pip python3-venv

WORKDIR /app

# Create virtual environment
RUN python3 -m venv venv1

# Activate venv and install dependencies
RUN /bin/bash -c "source venv1/bin/activate && pip install --no-cache-dir -r requirements.txt"


################################################
# Final image
################################################
FROM ubuntu

WORKDIR /app
# Copy the application and virtual environment
COPY --from=build /app /app

EXPOSE 8080
# Activate venv and run Django server
CMD ["/bin/bash", "-c", "source venv1/bin/activate && python3 manage.py runserver 0.0.0.0:8000"]