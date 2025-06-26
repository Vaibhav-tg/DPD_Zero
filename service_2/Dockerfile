# -------- Stage 1: Build -------
    FROM ghcr.io/astral-sh/uv:python3.13-bookworm-slim AS builder

    WORKDIR /app
    
    COPY pyproject.toml uv.lock ./
    
    RUN uv pip install --system .
    
    COPY app.py .
    
    # -------- Stage 2: Runtime --------
    FROM python:3.13-slim
    
    WORKDIR /app
    
    COPY --from=builder /usr/local /usr/local
    
    COPY --from=builder /app/app.py .
    
    EXPOSE 8002
    
    CMD ["python", "app.py"]
    