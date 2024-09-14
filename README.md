# Question-Answering AI

## Project Description

This project implements a question-answering system using the Hugging Face Transformers library and Gradio. The system allows users to interact with an AI model that can answer questions based on a given context. The application supports both Arabic and English languages, leveraging pre-trained models specifically designed for question-answering tasks. The user can select the language, input context, and pose a question, and the AI will provide an appropriate answer.

## Installation

First, install the required libraries:

```bash
pip install gradio
pip install transformers
```

## Import Libraries

After installing, import the necessary libraries:

```python
from transformers import pipeline
import gradio as gr
```

## Download Models

Download two models: one for Arabic and one for English, and store them in variables:

```python
pipe_ar = pipeline("question-answering", model='ZeyadAhmed/AraElectra-Arabic-SQuADv2-QA')
pipe_en = pipeline("question-answering", model='deepset/roberta-base-squad2')
```

## Create Function

Define a function that takes three parameters:
- `lang`: The language selected by the user
- `text`: The context entered by the user
- `question`: The question entered by the user

The function will return the answer:

```python
def q_a(lang, text, question):
    if lang == 'Arabic':
        myinput = {
            'question': question,
            'context': text
        }
        return pipe_ar(myinput)['answer']
    elif lang == 'English':
        myinput = {
            'question': question,
            'context': text
        }
        return pipe_en(myinput)['answer']
```

## Gradio Interface

Create the Gradio interface:

- `fn` is the function
- `inputs` are:
  1. Language selection: `['Arabic', 'English']`
  2. Context
  3. Question

```python
app = gr.Interface(
    fn=q_a,
    inputs=[
        gr.Radio(['Arabic', 'English'], label='Select Language', value='Arabic'),
        gr.Textbox(label='Enter Text', lines=10),
        gr.Textbox(label='Enter Question')
    ],
    outputs=gr.Textbox(label='Answer')
)
```

## Run the App

To run the app:

```python
app.launch()
```
# Video Link
https://drive.google.com/file/d/1UNBufzd4xWPpjbtYv2Z8epz7hrugJuDU/view?usp=share_link
