FROM python:3.9
WORKDIR /app
COPY . .
RUN poetry install --no-dev
CMD ["gunicorn", "--bind", "0.0.0.0:9000", "tracking_project.wsgi"]