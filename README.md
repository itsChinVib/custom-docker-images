# Docker Images for personal use


1. LLMEnvironment
    - Image Name: chinvib66/llm-ubuntu-llamacpppython-pgvector
    - Contains the following packages
        - NVIDIA Cuda Toolkit 12.1
        - Langchain
        - LLamaIndex
        - LLama-cpp-python
        - Gradio
        - Unstructured IO and dependencies
    - Contains following Models
        - [WhereIsAI/UAE-Large-V1](https://huggingface.co/WhereIsAI/UAE-Large-V1)
        - [mistral-7b-instruct-v0.1.Q5_K_M.gguf](https://huggingface.co/TheBloke/Mistral-7B-Instruct-v0.1-GGUF/resolve/main/mistral-7b-instruct-v0.1.Q5_K_M.gguf)
    - MODEL_DIR env variable is path to dir where models are stored
    - MODEL_DIR = '/app/models'
