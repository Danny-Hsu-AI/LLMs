import os
import google.generativeai as genai
from google.generativeai.types import GenerationConfig

def generate_answer(prompt: str, temperature: float, max_tokens: int):
    """Generate answer using Gemini Pro API with temperature and max_tokens"""
    gemini_api_key = os.getenv("GEMINI_API_KEY")
    if not gemini_api_key:
        raise ValueError("Gemini API Key not provided. Please provide GEMINI_API_KEY as an environment variable")
    
    genai.configure(api_key=gemini_api_key)
    model = genai.GenerativeModel('gemini-pro')
    
    generation_config = GenerationConfig(
        temperature=temperature,
        max_output_tokens=max_tokens
    )
    
    result = model.generate_content(prompt, generation_config=generation_config)
    return result.text
