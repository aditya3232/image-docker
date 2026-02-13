# kalau mau run langsung prometheus
docker run -d \
        --name prometheus \
        -p 9090:9090 \
        --add-host=host.docker.internal:host-gateway \
        prom/prometheus

# kalau mau run grafana langsung
