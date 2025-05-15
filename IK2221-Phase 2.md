#PASSWORD: `BnxxcLJTDmgR`
# 1. Sys init
# Connect SSH
1. Open terminal
2. Connect ssh
```
ssh ik2221-server
```
3. password
```
BnxxcLJTDmgR
```
## Tmux setting
1. Create new tmux session `ik2221`
```
tmux new -s ik2221
```
- Can attach a session to retrieve the work
```
tmux attach -t ik2221
```
- Detach session, don't use `exit` it will kill all serverice
```
tmux detach
```
2. Split 4 windows horizional
```
tmux split-window -h
```
3. To move within windows, press `ctrl + b` first, then use arrow to move
4. On Terminal 1:
```
source venv/bin/activate
PYTHONPATH="$(pwd)/LMCache:$(pwd)/lmcache-vllm-extended:$PYTHONPATH"
export PYTHONPATH
cd lmcache-server/
python -m lmcache_server.server 192.168.2.30 65432 ./
```
5. On Terminal 2:
```
source venv/bin/activate
PYTHONPATH="$(pwd)/LMCache:$(pwd)/lmcache-vllm-extended:$PYTHONPATH"
export PYTHONPATH

cd lmcache-vllm-extended
LMCACHE_CONFIG_FILE="configuration.yaml" \
CUDA_VISIBLE_DEVICES=0 \
python lmcache_vllm/script.py serve \
Qwen/Qwen2.5-1.5B-Instruct \
--gpu-memory-utilization 0.8 \
--dtype half \
--port 8000
```
6. When Process in terminal 2 compelte, On Terminal 3:
```
source venv/bin/activate
PYTHONPATH="$(pwd)/LMCache:$(pwd)/lmcache-vllm-extended:$PYTHONPATH"
export PYTHONPATH

cd /home/ik2221vt25g02/lmcache-vllm-extended/frontend
streamlit run frontend.py
```
7. On Terminal 4:
- GPU usage monitoring (-d flag highlights differences between the outputs)
```
watch -d -n 0.5 nvidia-smi
```
8. Visit the frontend on 
```
http://localhost:8501
```
# Others attach the session
## Open terminal
## 1. Attach session
```
tmux a -t ik2221
```
## 2. Detach session (Don't use `exit`!!!)
```
tmux detach
```
## 3. Move between windows:
1. Press `ctrl/control + b`
2. use ⬆️ ⬇️ ⬅️ ➡️ to move

## 4. Scroll up and down in tmux
1. Press `Ctrl + b`
2. Press `[` (left square bracket).
3. To return to exit mode, press `q`
