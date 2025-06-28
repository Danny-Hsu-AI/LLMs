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

# gemini_temperature_test.py

import os
import google.generativeai as genai
from google.generativeai.types import GenerationConfig

def generate_answer(prompt: str, temperature: float, max_tokens: int):
    """Generate answer using Gemini Pro API with temperature and max_tokens"""
    gemini_api_key = os.getenv("AIzaSyDceM6k-RNXffnGd-l0-EcMbLxZHL88GZA")
    if not gemini_api_key:
        raise ValueError("❌ Gemini API Key not provided. Please set GEMINI_API_KEY as an environment variable.")
    
    genai.configure(api_key=gemini_api_key)
    model = genai.GenerativeModel('gemini-pro')

    generation_config = GenerationConfig(
        temperature=temperature,
        max_output_tokens=max_tokens
    )

    result = model.generate_content(prompt, generation_config=generation_config)
    return result.text

def main():
    final_prompt = "Explain what artificial intelligence is in simple terms."
    temperatures = [0.0, 0.5, 1.0]
    max_tokens = 200

    for temp in temperatures:
        print("\n" + "=" * 50)
        print(f"🔥 Temperature: {temp}")
        print("=" * 50)
        try:
            response = generate_answer(final_prompt, temperature=temp, max_tokens=max_tokens)
            print(response.strip())
        except Exception as e:
            print(f"❌ Error at temperature {temp}: {e}")

if __name__ == "__main__":
    main()
