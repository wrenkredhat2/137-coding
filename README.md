# 137-coding



Setup:

sudo dnf install intel-gpu-tools
sudo intel_gpu_top


sudo systemctl edit ollama.service

INsertonto NEW-Section:


[Service]
Environment="OLLAMA_INTEL_GPU=1"


sudo systemctl daemon-reload
sudo systemctl restart ollama.service
sudo intel_gpu_top
sudo dnf install htop

sudo dnf install mesa-vulkan-drivers vulkan-loader

sudo dnf install vulkan-tools
vulkaninfo --summary


export VK_ICD_FILENAMES=/usr/share/vulkan/icd.d/intel_anv_icd.x86_64.json
export OLLAMA_INTEL_GPU=true
export OLLAMA_VULKAN=1

podman run -d \
  --device /dev/dri \
  --security-opt label=disable \
  -e VK_ICD_FILENAMES="/usr/share/vulkan/icd.d/intel_icd.x86_64.json" \
  -e OLLAMA_INTEL_GPU="true" \
  -e OLLAMA_IGPU_ENABLE="1" \
  -e OLLAMA_VULKAN="1" \
  -v ollama:/root/.ollama \
  -p 11434:11434 \
  --name ollama-intel \
  docker.io/ollama/ollama:latest

ollama run qwen2.5:1.5b "Schreibe ein Gedicht über Linux."


Environment="OLLAMA_IGPU_ENABLE=1"

ollama run llama3.2:1b

ollama create qwen-power -f ./Modelfile.conf

ollama pull qwen2.5-coder:7b

ollama create coder-pro -f ./Modelfile_qwen2.5-coder:32b.conf

### Sublemental
https://medium.com/@leyesvalentinasofia/ollama-step-by-step-tutorial-with-demo-project-4bdca78f8833