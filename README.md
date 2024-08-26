# LLM-Text-Masking-to-protect-Sensitive-Data
In this we hide the sensitive data using GEMINI LLM

## Introduction
In today's data-driven world, large unstructured documents are common in many industries, such as finance, healthcare, and legal services. These documents often contain a mix of relevant and irrelevant information, making it challenging to extract the necessary details without being overwhelmed by extraneous data.

When working with sensitive data, it’s crucial to protect this information. Masking or removing unwanted text helps maintain privacy, comply with regulations like GDPR, and streamline content for analysis.

Large Language Models (LLMs), such as GPT-3.5 or Gemini, have proven effective tools for identifying and masking these unwanted text segments in an automated fashion. Their ability to understand context and semantics allows them to outperform traditional rule-based methods.

## Understanding Masking and Its Importance

### What is Masking?
Masking refers to the process of obscuring or removing specific parts of a text. This is particularly important in scenarios involving data privacy, where sensitive information (e.g., personal identifiers like names, phone numbers, email addresses, social security numbers, or confidential details) needs to be hidden to protect individuals' privacy or to secure corporate data.

### Why Use LLMs for Masking?
Traditional methods for masking involve regular expressions or rule-based systems, which can be effective but also brittle. These methods often fail when dealing with complex text patterns, varied formats, or when the context is necessary to determine what should be masked.

LLMs, such as GPT-3.5 or Google’s Gemini, provide a more robust solution. They can understand the context and meaning behind the text, allowing them to more accurately identify which parts of the text should be masked.

## Example Document
Consider the following unstructured document:
```
Dear Pavan Somisetty,

Your social security number is 123-45-6789. Please keep it safe.

Also, note that your appointment with the manager is scheduled for tomorrow at 10 AM.

Best regards, Pavan Somisetty
```


In this document, sensitive information includes the name "Pavan Somisetty" and the social security number "123-45-6789". A masking function would identify these elements and replace them with a placeholder, ensuring that the document can be shared or analyzed without exposing private details.

## Masking with Gemini
This function uses the Google Gemini model to automatically mask sensitive information in a document. The process involves sending a carefully crafted prompt to the LLM, asking it to identify and mask sensitive details such as names, phone numbers, email addresses, and credit card numbers.

The model returns the modified document with sensitive information replaced by a mask token (e.g., `[MASK]`). This automated approach leverages the LLM's understanding of context to ensure that the right elements are masked.

### Code Example
```python

import pandas as pd
import warnings
import os
from dotenv import load_dotenv,find_dotenv
import google.generativeai as genai
import getpass
# Set the API key and Gemini model name directly in the code

model_name = "gemini-1.5-flash"
api_key = getpass.getpass("Enter your Google Gemini API key: ")
# Ensure the API key is set
if not api_key:
    raise ValueError("API_KEY must be set.")

# Configure the generative AI client
genai.configure(api_key=api_key)

print(f"Using MODEL={model_name}")

# Sample unstructured document
document = """
Dear Pavan Somisetty,

Your social security number is 123-45-6789. Please keep it safe.

Also, note that your appointment with manager is scheduled for tomorrow at 10 AM.

Best regards,
Pavan Somisetty
"""
import google.generativeai as gemini

def mask_unwanted_text_gemini(document, mask_token="[MASK]"):
    # Set up the prompt for the Gemini model
   
     response = model.generate_content(f"Please mask any sensitive information like name, phone numbers, email addresses, or credit card numbers in the following text, replacing them with '{mask_token}':\n\n{document}")
  
    # Return the masked document
     return response.text


masked_document = mask_unwanted_text_gemini(document)
print(masked_document)



```
 and this can also can be done Text masking on documents also this will be in code as:

 ```python
import pandas as pd
import warnings
import os
from dotenv import load_dotenv,find_dotenv
import google.generativeai as genai
import getpass
# Set the API key and Gemini model name directly in the code

model_name = "gemini-1.5-flash"
api_key = getpass.getpass("Enter your Google Gemini API key: ")
# Ensure the API key is set
if not api_key:
    raise ValueError("API_KEY must be set.")

# Configure the generative AI client
genai.configure(api_key=api_key)

print(f"Using MODEL={model_name}")
import PyPDF2
def extract_text_from_pdf(pdf_path):
    with open(pdf_path, 'rb') as file:
        reader = PyPDF2.PdfReader(file)
        text = ''
        for page in reader.pages:
            text += page.extract_text()
    return text

# Example usage
pdf_path = r'C:\Users\pavan\OneDrive\Desktop\PAVAN SOMISETTY.pdf'#path to your document
document = extract_text_from_pdf(pdf_path)
import google.generativeai as gemini

def mask_unwanted_text_gemini(document, mask_token="[MASK]"):
    # Set up the prompt for the Gemini model
   
     response = model.generate_content(f"Please mask any sensitive information like name, phone numbers, email addresses, or credit card numbers in the following text, replacing them with '{mask_token}':\n\n{document}")
  
    # Return the masked document
     return response.text


masked_document = mask_unwanted_text_gemini(document)
print(masked_document)
```


### Collect and Label Data
If the basic masking function does not meet your specific needs, consider fine-tuning the LLM on your dataset. Begin by collecting a dataset of documents where the text you want to mask is labeled accordingly.

### Fine-Tune the LLM
Use a platform like Hugging Face's Transformers library or Gemini's fine-tuning API to train the model. Fine-tuning enhances the model's accuracy, especially for domain-specific documents.

### Deploy and Test
Deploy the fine-tuned model within your system to automatically mask unwanted text in documents. Make sure to test the model thoroughly to ensure it masks the correct text without removing relevant details.

## Best Practices and Considerations

### Contextual Awareness
Ensure that the model understands the document's context. Overzealous masking might remove important information that is not sensitive but contextually important.

### Testing and Validation
Always validate the output of your masking system, either manually or through automated tests, to ensure accuracy.

### Ethical Considerations
Comply with data privacy regulations (e.g., GDPR, HIPAA). Anonymize data where possible and be mindful of the ethical implications of processing sensitive information.

## Conclusion
Masking unwanted text in unstructured documents is crucial for data privacy, content management, and legal compliance. Large Language Models (LLMs) like Google’s Gemini offer a powerful tool for automating this process, providing flexibility and contextual understanding that traditional methods lack.

By following this guide, you can set up a basic masking system using LLMs and customize it to your specific needs. Fine-tuning models can further enhance performance and efficiency, ensuring your data remains secure and appropriately managed.
ent
 

