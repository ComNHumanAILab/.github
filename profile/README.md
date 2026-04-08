# `docker-compose 설정`

```yaml
services:
  postgres-db:
    container_name: postgres-cnh
    image: pgvector/pgvector:pg16
    environment:
      POSTGRES_USER: CnH
      POSTGRES_PASSWORD: 1q2w3e4r!!
      POSTGRES_DB: CnHAssistant
    ports:
      - "5432:5432"
    volumes:
      - postgres_data:/var/lib/postgresql/data

  langchain-app:
    container_name: langchain-app
    image: chain-app:v1_0_0
    network_mode: host
    working_dir: /app/llm_inf/langchain_app/src
    volumes:
      # llm_inf 아래 모든 파일 마운트
      - ./llm_inf:/app/llm_inf
      # 데이터 입출력 폴더 마운트
      - /hdd_data/user_input_folder:/hdd_data/user_input_folder
      - /hdd_data/llm_output_folder:/hdd_data/llm_output_folder
      - /hdd_data/generated_images:/hdd_data/generated_images
    command: ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]


```
