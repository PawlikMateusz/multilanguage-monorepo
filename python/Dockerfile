FROM python:3.8 AS builder
ARG project

WORKDIR /build

COPY $project/requirements.txt .

RUN pip3 install --user -r requirements.txt

# second unnamed stage
FROM python:3.8-slim
WORKDIR /app

COPY --from=builder /root/.local/bin /root/.local
ENV PATH=/root/.local:$PATH

COPY ./entry_point.sh ./app ./

CMD [ "bash", "entry_point.sh" ]