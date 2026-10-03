# Developer Cookbook — PAX_REASONING
**Stack:** Python 3.11, PAX 27B, ReAct framework, AIOSS_FORMAT

## Basic Usage
```python
from pax_reasoning import Reasoning
module = Reasoning(pax_model="./pax-27b-q4.gguf",
                               aioss_chain="./pax_reasoning.aioss")
result = module.process(input_data)
print(result.output, result.chain_hash)
```

## Batch Processing
```python
results = module.process_batch(inputs, batch_size=4)
for r in results:
    print(r.chain_hash)
```

## AIOSS Append
```python
import hashlib, time
def aioss_append(chain_path, payload: bytes, module_id: str):
    entry_hash = hashlib.sha3_256(payload).digest()
    ts = int(time.time_ns()).to_bytes(8, 'big')
    with open(chain_path, 'rb') as f:
        f.seek(-32, 2); prev_hash = f.read(32)
    new_hash = hashlib.sha3_256(prev_hash + entry_hash + ts).digest()
    with open(chain_path, 'ab') as f:
        f.write(ts + entry_hash + new_hash)
    return new_hash.hex()

chain_hash = aioss_append("./pax_reasoning.aioss", result.to_bytes(), "PAX_REASONING")
```

## Integration with Anticloud TIER_2
```python
# Chain with PAX_INFERENCE_CORE
from pax_inference_core import PAXInferenceCore
from pax_reasoning import Reasoning

core = PAXInferenceCore(model="./pax-27b-q4.gguf")
module = Reasoning(inference_core=core)
```

## Domain: Multi-hop reasoning and chain-of-thought module for PAX 27B
This module specializes in: multi-hop reasoning and chain-of-thought module for pax 27b.
AIOSS entry type: reasoning trace (premises hash + inference steps hash + conclusion hash + confidence).

## Performance
Use module.benchmark() to measure throughput on your hardware.
Pre-warm: module.warmup() before serving production requests.
