# 👨‍💻👨‍🏫 Code Explainer with Generative Ai 🤖📚

### 1️⃣ Import required Libraries
``` python 
import google.generativeai as plam
import os
```
### 2️⃣ Configure Api key
``` python 
plam.configure(api_key='xxxxxxxxxxxxxxxxxx')
```

### 3️⃣ Select the model(generate text)
```python
models=[m for m in plam.list_models() if 'generateText' in m.supported_generation_methods]
model=models[0].name
model
```
models/text-bison-001

#### Sample Prompting🧪
``` python
input_prompt='What is prompt engineering?'
```

##### Here we use gererate_text function to retrive the information from generative ai
``` python 
Ans=plam.generate_text(
    model=model,
    prompt=input_prompt,
    temperature=0, #for more determinastic result and 1 for more randomness result
    max_output_tokens=100
)
Ans.result
```

