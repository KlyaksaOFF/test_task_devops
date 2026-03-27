FROM python:3.13-slim
LABEL authors="alex"
EXPOSE 8080

COPY --from=ghcr.io/astral-sh/uv:0.11.1 /uv /uvx /bin/

WORKDIR /app

COPY pyproject.toml ./
COPY uv.lock ./

RUN uv sync

COPY . .

CMD ["uv", "run", "uvicorn", "backend.app:app", "--host", "0.0.0.0", "--port", "8080"]