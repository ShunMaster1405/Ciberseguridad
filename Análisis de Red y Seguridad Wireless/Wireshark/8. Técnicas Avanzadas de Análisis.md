## Análisis de Patrones de Tráfico

### Identificación de Comportamiento Anómalo

#### Volumen de Tráfico Inusual

```bash
frame.len > 1500
tcp.analysis.bytes_in_flight > 65535
```

#### Patrones de Temporización

```bash
tcp.time_delta < 0.001
frame.time_delta > 60 and frame.time_delta < 65
```

## Correlación de Eventos

### Análisis Temporal

```bash
dns.qry.name == "malicious.com"
http.host == "malicious.com"
```

```bash
ip.src == 192.168.1.100 and (http or https or ftp)
```

### Análisis de Cadenas de Infección

1. Identificar punto de entrada inicial
2. Seguir comunicaciones subsecuentes
3. Mapear propagación lateral
4. Documentar indicadores de compromiso

## Automatización con Scripts

### Uso de tshark (CLI)

```bash
tshark -r capture.pcap -Y "http.request" -T fields -e http.host -e http.request.uri
tshark -r capture.pcap -T fields -e ip.src -e ip.dst | sort | uniq
tshark -r capture.pcap --export-objects http,./extracted_files/
```