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
<p>Prompt engineering is the process of designing and implementing prompts that can be used to guide language models to generate specific kinds of text. This can be used for a variety of purposes, such as generating creative content, completing tasks, or answering questions. Prompt engineering is a relatively new field, and there is still a lot of research to be done. However, it has the potential to be a powerful tool for creating new kinds of language models and applications.</p>

### 4️⃣ Make Response Function
We make this function to get response from generative ai API
``` python 
def get_Response(prompt):
  Ans=plam.generate_text(
    model=model,
    prompt=prompt,
    temperature=0, #for more determinastic result and 1 for more randomness result
    max_output_tokens=500
  )
  response=Ans.result
  return response
```
### 5️⃣ Input the code snippet
``` python
Input_code=f"""
X=10
if(X>0):
  print("X is positive")
else:
  print("X is Negative")
"""
```

### 6️⃣ Prepare the prompt
``` python
prompt=f"""
Your task is to act as a Python Code Explainer.
I'll give you a code Snippet.
Your job is to explain the code in simplest way with steps.
Also, give the final result of the code with reason.
Code snippet is shared below, delimited with triple backticks:
-```-
{Input_code}
-```-
"""
print(prompt)```

