FROM gcc:latest
RUN apt-get update && apt-get install -y --no-install-recommends build-essential curl netcat-traditional libc6-dbg

# Copy in source code
WORKDIR /app
COPY src src

# TEST vs PROD builds
RUN gcc -o gps_uploader -g -fsanitize=undefined src/gps_uploader.c

# Some demo example GPS data
COPY gps_data.txt /testsuite/gps_data.txt
COPY gps_data.txt .

CMD ["/app/src/wait-for-it.sh", "api", "--", "/app/gps_uploader", "/testsuite/gps_data.txt", "http://api:8000/location"]
