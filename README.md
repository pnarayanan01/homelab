# Strix Halo AI Stack

Local AI setup on GMKTEC EvoX2 with AMD Strix Halo (128GB unified memory).

## Services

| Service | Port | Description |
|---------|------|-------------|
| Ollama | 11434 | LLM inference server |
| Open WebUI | 8080 | Chat interface |
| ComfyUI | 8188 | Image generation |

## Setup

### Kernel parameters (in /etc/default/grub)
```
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash amd_iommu=off amdgpu.gttsize=126976 ttm.pages_limit=32505856"
```

### Install ComfyUI systemd service
```bash
sudo cp comfyui.service /etc/systemd/system/
sudo systemctl daemon-reload
sudo systemctl enable comfyui
sudo systemctl start comfyui
```

### Start Open WebUI
```bash
docker compose up -d
```

## Useful commands
```bash
# Status
sudo systemctl status ollama comfyui
docker ps

# Logs
journalctl -u comfyui -f
docker logs -f open-webui

# Ollama models
ollama list
ollama pull llama3.3:70b
```
