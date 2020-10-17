FROM python:3.8 AS builder

ARG project
ENV PATH="/venv/bin:$PATH"

RUN python3 -m venv /venv
COPY $project/requirements.txt .

RUN pip3 install --no-cache-dir -r requirements.txt

# second unnamed stage
FROM python:3.8-slim

ARG project
ENV PATH="/venv/bin:$PATH"

COPY --from=builder /venv /venv

WORKDIR /app

COPY $project/entry_point.sh .
COPY $project/app ./app

CMD [ "bash", "entry_point.sh" ]