# Use latest python
FROM python:3.11

# Ensures python output is unbuffered when written out
ENV PYTHONUNBUFFERED 1

# System dependencies
RUN apt-get update && apt-get install -y netcat-traditional

# Create aforum user
RUN addgroup --system aforum && adduser --system --group --home /home/aforum aforum
ENV PATH="${PATH}:/home/aforum/.local/bin"

# Create backend directory
RUN mkdir /api
RUN mkdir /api/staticfiles

# Set backend directory to working directory
WORKDIR /api

# Copy project files to /backend
COPY . /api/
RUN chmod +x /api/entrypoint.sh
RUN chown -R aforum:aforum /api/

# Change to aforum user
USER aforum

# Install requirements
RUN pip install --upgrade pip
RUN pip install -r requirements.txt

ENTRYPOINT ["/api/entrypoint.sh"]
