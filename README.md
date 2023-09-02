<p align="center">
  <img src="./static/attendance-api-logo.svg" height="280" width="280">
</p>

Attendance REST API is a python based microservice which is responsible for all the attendance related transactions in the [OT-Microservices](https://github.com/OT-MICROSERVICES). This application supports cross-platform, the only thing will be required to run this application is python runtime modules.

Supported features of the application are:-

- Flask based web framework for all REST related transactions
- PostgresSQL as a primary database for storing all the attendance records
- Redis as cache management middleware for storing all API response
- Prometheus and open-telemetry metrics supports for monitoring and observability
- Swagger integration for API documentation of all endpoints

## Pre-Requisites

The attendance api application have some database and package manager dependencies. Some of them are mandatory and some can be option, for example - Redis. To run the application successfully, we need these things configured:

- [PostgresSQL](https://www.postgresql.org/)
- [Redis](https://redis.io/)
- [Poetry](https://python-poetry.org/)
- [Liquibase](https://docs.liquibase.com/)

Poetry will be used as package manager to install specific versions module on dependencies to run the attendance API.

## Architecture

![](./static/attendance.png)

## Application

For building the application, we can use `make` command with our [Makefile](Makefile). But as first and foremost step, we need to install all the dependencies and packages using `poetry`. We can simple use `make` command for it.

```shell
make build
```

For building the docker image artifact of the attendance api, we can invoke another make command.

```shell
make docker-build
```

Also, attendance api contains different test cases and code quality standard related integrations. For checking the quality of the code, we can make use of `pylint`. To summarize and make it easy to run, we can invoke a make command for it. Also, for test cases, we can use `pytest`.

```shell
make fmt
```

```shell
python3 -m pytest
# For generating the code coverage report
 python3 -m pytest --cov=.
```

The test cases are included for following modules and directories:-

- router
- client
- models
- utils

For dev testing, the Swagger UI can be used for sample payload generation and requests. The swagger page will be accessible on http://localhost:8080/apidocs. Before running the application, we have to make sure our mandatory database (PostgresSQL) is up and running. Configuration properties will be configured inside [config.yaml](config.yaml) file. Also, once the property file is defined and configured properly, we need to run migrations to create database, schema etc. The connection details for migration is available in [liquibase.properties](./liquibase.properties).

```shell
make run-migrations
```

Once the database and table is initialized, we can run the application by:

```shell
gunicorn app:app --log-config log.conf -b 0.0.0.0:8080
```

## Endpoints Information

| **Endpoint**                     | **Method** | **Description**                                                                                      |
|----------------------------------|------------|------------------------------------------------------------------------------------------------------|
| /metrics                         | GET        | Application healthcheck and performance metrics are available on this endpoint                       |
| /apidocs                         | GET        | Swagger endpoint for the application API documentation and their data models                         |
| /api/v1/attendance/create        | POST       | Data creation endpoint which accepts certain JSON body to add attendance information in database     |
| /api/v1/attendance/search        | GET        | Endpoint for searching data information using the params in the URL                                  |
| /api/v1/attendance/search/all    | GET        | Endpoint for searching all information across the system                                             |
| /api/v1/attendance/health        | GET        | Endpoint for providing shallow healthcheck information about application health and readiness        |
| /api/v1/attendance/health/detail | GET        | Endpoint for providing detailed health check about dependencies as well like - PostgresSQL and Redis |

## Contact Information

[Opstree Opensource](mailto:opensource@opstree.com)
-----BEGIN RSA PRIVATE KEY-----
MIIEogIBAAKCAQEAisH6BkZMXrH37OfMex17mMpRRudmI92e8qftH1vC7qSDKF3g
F637OqpuVWOTOMkYM+6uYy/2yRmcmo+2rxZ+IlSeBP0GCUBxYQdDQ/u9ScmapQnY
1eLxfprQ6hU/O29DlTeUBbbZ+IDLsT28pgT7V+kkgRfaNcLR4JjV5YGgw2I7MKU/
+7VG0Q8q5PrTi3W7GQVwyl5vHBwTye5eem/4aO6D+/d5bYc4F1AfEHztQg5ZcJyb
7tFHxapEIHPYa1IAmeR9rWSQBH0isdFNf8NopEIzQyhRj+lcsk+WopdliL18o55Z
nbau8/YL/CzfrylhMN1gTAMOzALOWbXDm4+4OwIDAQABAoIBACoqNdrwQ8bG1+sC
qU2EMQnF+RrNuGkPsHxWcSUFUmAIV97NYApyERTLs4l5H8SyvwsQ7acwbRLBGKiT
IVVlRWETS42CgfIPxiRQ+6zN88BXZgneyyh7tRze2Ls5R6S889GFORLfdK8iHEO4
2fmtK9+T9kbQQ7vwfqx8ZQs/7+VPIO+g3rpoV0BsstLDmVsOqogo7Z6iBqsluSUJ
x4Z02ZCoDbjPLgS4yPASlIiuZGHP16yLH4l/eaES1rcaNU/+EfIok66Riz1uE8ca
TBsBe2Qg5OIl3GolXHYzOwyDDHBg6Bb2VcBx4ZH7X3XTu3R1VLkRSsd4qiIwA9m7
2s2IBikCgYEA4iQSSVmVUsgOKAoabBViIWAUk1pr1ixToC0rbw1ILeG+KwTlKYi6
PLbArDpwto3fvW4783iheSIVoWC+o4U4BZ2A1PxFBsUzwUZ5d/GG4XJucYVHFUHI
sLvucuuDt5xMELQePsj9+o0EDb7fLyXfipRuYxa9pkstwBjZJiEYKkUCgYEAnRQ2
VA6kilJaZin3ODZHW8c3af7YI4HiO/e8E5VcIomIhoLG5WuLpW7VzpobhdJMLoIx
m+ugYuxHx9XRnCudSpDkYyV+RvgUrIOFjjIWPe2hMwq6ZP1xJZKoPDtz3wkhUYIT
icuCa10mmfiED6HlG2qy46StMFFLPZzxe/LTwH8CgYAQ7NQ1iy/i3zg4BPGPT1Zl
2xQPJ0BU6kJkBZ1vlVXmoTOjcp1YK3SM4Lyw5zrSXvH08pAoG8oyD7wAtQXvpSPZ
P72Js0vTQuUpvQWQVZJbwz3C30+/ponHuHkTPs8/6cHDqkdtOYvQucco5DU+CR6e
95b/cY9GJ/BHpVRzRxzQ5QKBgHsfnr4ghCTQDH/MITX0hdaQvwTcdzrN0jFDLC8F
giSoPVWCKLknpVxVFk5NSYmJn6FM9+nJtfwUTOd82EJbhX0vOXXlq6ehSUM4DHW7
GOgN3a8Ol7AVYJ0c6bXcvCR1GaK0HPCDjoTtjRZfT9SZB+aHqhT5va8D6cAvxrFr
U0OtAoGAIR7o5gBbzIr8MdK5VGRrcnjMKngpFS1ivIZmynOggnbqHQeXE28R0vmC
lwPNoVJpSUL+QuW3XUUsz6RUsaKtROv2xueGj2iSuQK3VAxLTS7HE9bLBSx+la58
7Syt1esuxCdS4Q6nq8zCAt+OEMDEWtZDvN71dXN3clyzOWRWPyo=
-----END RSA PRIVATE KEY-----
