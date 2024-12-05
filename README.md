# Conversational AI - aka Chatbot!
***
We created simple Chatbot application using the Gradio framework.

Please note: your Gradio screens may appear in `dark mode` or `light mode` depending on your computer settings.

![Chatbot](https://github.com/MihranD/Chatbot-ConversationalAI/blob/main/images/chatbot.png)

## Project Organization
----------------------------------------------------------------------------------------------
    ├── .gitignore          <- Includes files and folders that we don't want to control
    |
    ├── images              <- Images for use in this project
    │   ├── chatbot.png     <- Chatbot image
    │   └── result.png      <- Result image
    |
    ├── main.ipynb          <- Main jupyter file that needs to be run
    |
    ├── requirements.txt    <- The required libraries to deploy this project. 
    |                       Generated with `pip freeze > requirements.txt`
    └── README.md           <- The top-level README for developers using this project.

## Project Introduction

We will write a function `chat(message, history)` where:

**message** is the prompt to use  
**history** is the past conversation, in OpenAI format  

We will combine the system message, history and latest message, then call OpenAI. Gradio has been upgraded and it will pass in `history` in the exact OpenAI format, perfect for us to send straight to OpenAI.

### Model Output Example

```
system_message = "You are a helpful assistant in a clothes store. You should try to gently encourage \
the customer to try items that are on sale. Hats are 60% off, and most other items are 50% off. \
For example, if the customer says 'I'm looking to buy a hat', \
you could reply something like, 'Wonderful - we have lots of hats - including several that are part of our sales evemt.'\
Encourage the customer to buy hats if they are unsure what to get."
```

```
def chat(message, history):
    messages = [{"role": "system", "content": system_message}] + history + [{"role": "user", "content": message}]
    
    print("History is:")
    print(history)
    print("And messages is:")
    print(messages)
    print('\n')
    
    stream = openai.chat.completions.create(model=MODEL, messages=messages, stream=True)

    response = ""
    for chunk in stream:
        response += chunk.choices[0].delta.content or ''
        yield response
```

![Chatbot](https://github.com/MihranD/Chatbot-ConversationalAI/blob/main/images/result.png)

## Conclusion

Conversational Assistants are of course a hugely common use case for Gen AI, and the latest frontier models are remarkably good at nuanced conversation. And Gradio makes it easy to have a user interface. We covered how to use prompting to provide context, information and examples. Use the system prompt to give context on your business, and set the tone for the LLM.

## How to run the app

Follow these steps to set up and run the application:

1. **Create a `.env` file**  
   Add your OpenAI API key to the `.env` file in the following format:  
   ```plaintext
   OPENAI_API_KEY=sk-proj-blabla
   ```
   
2. **Setup virtual envirenment**  
   Run the following command to setup virtual envirenment:  
   ```bash
   python3 -m venv venv  # Create a virtual environment named 'venv'
   source venv/bin/activate  # Activate the virtual environment (Linux/Mac)'
   .\venv\Scripts\activate   # Activate the virtual environment (Windows)'
   ```

3. **Install Dependencies**  
   Run the following command to install all required dependencies:  
   ```bash
   pip install -r requirements.txt
   ```

4. **Open and Run the Notebook**  
   Open the `main.ipynb` file in Jupyter Notebook and execute the cells to run the application.

