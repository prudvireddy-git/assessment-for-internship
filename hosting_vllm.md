# Hosting a Fine-Tuned Qwen Model on a VPS Using vLLM

## Prerequisites

* Ubuntu 22.04 VPS
* NVIDIA GPU (recommended)
* CUDA Toolkit and NVIDIA Drivers
* Python 3.10+
* pip
* Fine-tuned Qwen model

---

## Step 1: Update the VPS

```bash
sudo apt update
sudo apt upgrade -y
```

---

## Step 2: Install Python and Git

```bash
sudo apt install python3 python3-pip git -y
```

---

## Step 3: Create a Virtual Environment

```bash
python3 -m venv vllm-env
source vllm-env/bin/activate
```

---

## Step 4: Install vLLM

```bash
pip install --upgrade pip
pip install vllm
```

---

## Step 5: Upload the Fine-Tuned Model

Copy the merged model to the VPS.

Example:

```
/home/ubuntu/models/vedaz_qwen_merged
```

---

## Step 6: Start the vLLM Server

```bash
python -m vllm.entrypoints.openai.api_server \
    --model /home/ubuntu/models/vedaz_qwen_merged \
    --host 0.0.0.0 \
    --port 8000
```

---

## Step 7: Verify the Server

```bash
curl http://localhost:8000/v1/models
```

The server should return the loaded model information.

---

## Step 8: Test Chat Completion

```bash
curl http://localhost:8000/v1/chat/completions \
-H "Content-Type: application/json" \
-d '{
  "model":"vedaz_qwen_merged",
  "messages":[
    {
      "role":"user",
      "content":"Will I get a promotion this year?"
    }
  ]
}'
```

---

## Production Recommendations

* Configure Nginx as a reverse proxy.
* Enable HTTPS using Let's Encrypt.
* Use a systemd service to automatically restart the server.
* Monitor GPU utilization with:

```bash
nvidia-smi
```

---

## Conclusion

Using vLLM provides efficient GPU memory usage, fast inference through continuous batching, and an OpenAI-compatible API, making it suitable for serving a fine-tuned Qwen model in production.
