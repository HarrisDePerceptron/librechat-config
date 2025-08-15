
## Getting Started
Make sure ollama is accepting at 0.0.0.0
```
systemctl edit ollama.service
```
```
[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"
```

reload
```
systemctl daemon-reload
systemctl restart ollama
```


### Start server
```
./run.sh
```
