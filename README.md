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
print(prompt)
```

### 7️⃣ Get Response
``` python 
Response=get_Response(prompt)
print(Response)
```

-# This code is to check if the value of variable X is positive or negative.

1. The variable X is assigned the value 10.
2. The if statement checks if the value of X is greater than 0.
3. If the value of X is greater than 0, the print statement "X is positive" is executed.
4. If the value of X is not greater than 0, the print statement "X is Negative" is executed.

The final result of the code is "X is positive" because the value of X is greater than 0.

## Make an Interface for This Explainer 🎴

### install gradio 
``` python
!pip install gradio
```

### make interface using gradio
``` python
import gradio as gr
import os
import google.generativeai as plam

#Configure API key
plam.configure(api_key='AIzaSyByPkcLmF72Itb1yX17F6L65sg4Z4bq904')

#select model
models=[m for m in plam.list_models() if 'generateText' in m.supported_generation_methods]
model=models[0].name


#Get response function
def get_Response(input_txt):
  prompt=f"""
  Your task is to act as a Python Code Explainer.
  I'll give you a code Snippet.
  Your job is to explain the code in simplest way with steps.
  Also, give the final result of the code with reason.
  Code snippet is shared below, delimited with triple backticks:
  -```-
  {input_txt}
  -```-
  """
  Ans=plam.generate_text(
    model=model,
    prompt=prompt,
    temperature=0, #for more determinastic result and 1 for more randomness result
    max_output_tokens=500
  )
  response=Ans.result
  return response


#For interface
iface=gr.Interface(fn=get_Response,inputs=[gr.Textbox(label="Insert code Snippet",lines=8)],outputs=[gr.Textbox(label="Explanation here",lines=8)],title="Python Code Explainer")

iface.launch(share=True,debug=True)
```

## Screens
### 1. Code explainer
<kbd>![image](https://github.com/Nimisha-Mavar/Python_Code_Explainer/assets/112267753/05c334d0-fd17-4d8e-bab5-f41648eb8325)</kbd>

### 2. Even Odd number  
<kbd>![image](https://github.com/Nimisha-Mavar/Python_Code_Explainer/assets/112267753/66c6101f-29dd-4b3f-9d02-cb0c77e5ee74)
</kbd>
