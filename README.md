# ReX: An Interactive Assistant Powered by Google Gemini

This repository contains a simple web application built using Streamlit and Vertex AI. The application showcases a chat interface with ReX, an interactive assistant powered by Google Gemini. ReX introduces itself, interacts using emojis, and responds to user inputs.

## Features

- **Interactive Chat Interface**: Engage with ReX through a web-based chat interface.
- **Personalized Greetings**: ReX provides personalized greetings based on user input.
- **Session Management**: Keeps track of the conversation using Streamlit's session state.

## Prerequisites

- Python 3.7 or later
- Streamlit
- Vertex AI SDK

## Installation

1. **Clone the repository:**

    ```bash
    git clone https://github.com/vengotimuktha/rex-interactive-assistant.git
    cd rex-interactive-assistant
    ```

2. **Install the required packages:**

    ```bash
    pip install -r requirements.txt
    ```

3. **Set up Vertex AI:**

    Ensure you have access to Google Cloud Platform and have set up Vertex AI. Update the `project` variable in the code with your Google Cloud project ID.

## Usage

1. **Run the Streamlit app:**

    ```bash
    streamlit run app.py
    ```

2. **Interact with ReX:**

    Open the provided URL in your browser (usually `http://localhost:8501`), enter your name, and start chatting with ReX.

## Code Overview

### Import Libraries

```python
import vertexai
import streamlit as st
from vertexai.preview import generative_models
from vertexai.preview.generative_models import GenerativeModel, Part, Content, ChatSession

### Initialize Vertex AI
project = "sample-gemini"
vertexai.init(project=project)

###Configuring Generative Model
config = generative_models.GenerationConfig(
    temperature=0.4
)
model = GenerativeModel(
    "gemini-pro",
    generation_config=config
)
chat = model.start_chat()

### Streamlit App Code
import streamlit as st
from vertexai.preview.generative_models import GenerativeModel, GenerationConfig

### Initialize Session State
if 'messages' not in st.session_state:
    st.session_state.messages = []

### Function to send Messages
def llm_function(chat, message):
    st.session_state.messages.append(message)

###Initialize the Generative Model for Chat
model = GenerativeModel("gemini-pro")


### Implement Logic for Initial Prompt
if len(st.session_state.messages) == 0:
    initial_prompt = "Introduce yourself as ReX, an assistant powered by Google Gemini. You use emojis to be interactive"
    llm_function(chat, initial_prompt)

###Chat Interface
chat = st.empty()  # Create an empty slot for the chat interface

### Streamlit App Interface
st.title("Welcome to ReX, Your Assistant")
user_name = st.text_input("Please enter your name")
if user_name:
    personalized_greeting = f"Hello, {user_name}! I'm ReX, your assistant powered by Google Gemini. 😊"
    llm_function(chat, personalized_greeting)

### Displaying Personalized Greetings Based on User Input
if len(st.session_state.messages) > 1:
    last_message = st.session_state.messages[-1]
    if "name" in last_message.lower():
        llm_function(chat, "Nice to meet you, I'm ReX! How can I assist you today?")

Contributing
Feel free to fork this repository, create a branch, and submit pull requests. Any contributions to enhance ReX are welcome!

License
This project is licensed under the MIT License - see the LICENSE file for details.

Acknowledgements
Streamlit
Vertex AI
Google Cloud Platform


