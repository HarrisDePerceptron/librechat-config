
## Getting Started
#Make sure ollama is accepting at 0.0.0.0

systemctl edit ollama.service

`[Service]
Environment="OLLAMA_HOST=0.0.0.0:11434"`


systemctl daemon-reload
systemctl restart ollama



### Start server
git clone https://github.com/danny-avila/LibreChat.git

#Copy all files in this directory to the main repo

cp ./* /path/to/LibreChat

cd path/to/LibreChat

./run.sh
