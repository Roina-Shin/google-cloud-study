### [Source of this study material : Google Generative AI: Gemini API, Gen AI Studio, Bard & More by Colt Steele](https://www.udemy.com/course/google-generative-ai/)


## How to get started with Bard

- Head over to [Bard](https://bard.google.com/chat) and clcik Try to get started.


![bard-interface](/GCP_pictures/AI/Bard/bard-interface.PNG "Bard interface")


- It's very similar to how Chat GPT works. You ask a question and Bard gives you an answer.


![prompt-bard](/GCP_pictures/AI/Bard/prompt-bard.PNG "Prompt Bard")


- What's cool about Bard is that you can play audio on the text answer and also get other draft versions of the answer.


![drafts-and-audio](/GCP_pictures/AI/Bard/drafts-and-audio.PNG "Bard offers audio feature and a few drafts of answer")


- When I give it an image and asks what it is as well as what car model it is, it gave me the correct answer:


![image-processing](/GCP_pictures/AI/Bard/image-processing.PNG "Bard is good at image processing")


- You can actually speak your prompts using the speaker icon as well:


![speak-prompt](/GCP_pictures/AI/Bard/speak-prompt.PNG "Speak your prompt")


- If you use Google Drive, Docs, and gmail, you can connect Bard to those services.


![enable-google-workspace](/GCP_pictures/AI/Bard/enable-google-workspace.PNG "Enable Google Workspace extension")


- Once enabled, you can prompt something like this:


![prompt-emails](/GCP_pictures/AI/Bard/email-prompt.PNG "Prompt the emails you got")



## How to get started with Google AI Studio

- Instead of Bard's chat-like interface, **Google AI Studio** provides you with different parameters and model selection, etc. that you can go with a single prompt.

- Google AI Studio is a browser based IDE that you can use to build AI model using Gemini.


 ### Signing up for Google AI Studio

  - Go over to this [sign up](https://makersuite.google.com/app/prompts/new_freeform) link and consent to the service terms:


  ![google-ai-studio-interface](/GCP_pictures/AI/Google-AI-Studio/google-ai-studio-interface.PNG "Google AI Studio Interface")


  - On the right side panel, you can opt for Gemini Pro or Gemini Pro Vision.


  ![gemini-versions](/GCP_pictures/AI/Google-AI-Studio/gemini-versions.PNG "Gemini Pro and Gemini Pro Vision")


  - **Gemini Pro**

    - Input: text
    
    - Output: text

    - Input token limit: 30,720

    - Output token limit: 2,048

    - Rate limit: 60 requests per minute


  - **Gemini Pro Vision**

    - Input: text and/or image

    - Output: text

    - Input token limit: 12,288

    - Output token limit: 4,098

    - Rate limit: 60 requests per minute


 ### Gemini Pro - Test Input

   - You can actually test your prompt by adding various test variable to it. Surround the **test variable** with double curly braces **( {{}} )** so that you can test various values in one go.


  ![test-input](/GCP_pictures/AI/Google-AI-Studio/test-input.PNG "Test Input feature")



 ### Gemini Pro - Structured Prompt

   - You can provide an overall set of instructions for the model. In this case, you use **structured prompts**.


  ![structured-prompts](/GCP_pictures/AI/Google-AI-Studio/structured-prompt-in-menu.PNG "Opt for Structured Prompts")


  - You can make your marketing workflow much easier by using this structured prompts in Google AI Studio. Add some examples of Product Name and Product Descriptions up to 5. And also provide a product name that you want it to generate a product description for. Also write your prompt asking it to generate a product description given the provided examples:


  ![how-to-use-structurd-prompts](/GCP_pictures/AI/Google-AI-Studio/product-description-generator.PNG "How to use structured prompts for your marketing")



 ### Gemini Pro - Chat Prompt

   - Select the Chat Prompt from the Create New menu.


  ![chat-prompt](/GCP_pictures/AI/Google-AI-Studio/chat-prompt.PNG "Use the Chat Prompt")


  - You can train your chat prompt with example prompts you provided and then test your prompt with a new prompt:


  ![example-of-chat-prompt](/GCP_pictures/AI/Google-AI-Studio/chat-prompt.PNG "Provide example chat prompts to test your prompt")



 ### Gemini Pro Vision - Image Prompt

  - You can switch to the Gemini Pro Vision this time and test your Image prompt.


  ![image-prompt](/GCP_pictures/AI/Google-AI-Studio/image-prompt.PNG "Test your image prompt")


  - You can also ask other questions realted to the image prompt after prompt:


  ![other-image-prompts](/GCP_pictures/AI/Google-AI-Studio/more-image-prompts.PNG "More image prompts in one go")
 


 ### Gemini Pro Vision - Requirements

  - Maximum of 16 images per prompt

  - Maximum of 4MB for the entire prompt (including images and text)

  - No limit to the number of pixels in an image. Howeve, larger images are scaled down and padded to fit a maximum resolution of 3072 * 3072

  - Each image accounts for 258 tokens


 ### Gemini Pro Vision - Best Practices

  - Prompts with a single image tend to yield better results

  - If your prompt contains a single image, placing the image before the text prompt might produce better results

  - Images with higher resolution yield better results

  - Rotate images to their proper orientation before adding them to the prompt

  - If working with multiple images, label the images with text so you can refer to them within your prompt (e.g. image1: [image], image2: [image2])


 ### Temperature

  - Temperature controls the "randomness" in token selection.

  - It ranges from 0 to 1.

  - Higher temperature can lead to more diverse or creative results.

  - For example, if you are getting too similar responses, increase your temperatre.


 ### Stop Sequences

  - Stop if you generate one of these sequences.

  - Specifies a list of strings that tells the model to stop generating text if one of the strings is encountered in the response.

  - If a string appears multiple times in the response, then the response truncates where it's first encountered.

  - The stings are case sensitive.


  ![stop-sequence](/GCP_pictures/AI/Google-AI-Studio/stop-sequence.PNG "Stop Sequence feature")


 ### Top K

  - Top K goes from 1 to 40. The default Top K is set to 1.

  - While the temperature has the most immediate impact on your response, a lower Top K is focused on the model's output on a more specific set of options, reducing the likelihood of unexpected or irrelevant results.

  - A greater Top K promotes greater diversity in the model's output, especially when dealing with large and complex datasets.    


 ### Top P

  - Top K ranges from 0 to 1.

  - It's just another strategy of how the model selects tokens for output.

  - A lower Top P focuses the model's output on a narrower range of more likely options.

  - A higher Top P allows the model to generate more diverse and surprising outputs, while still maintaining some level of coherence and relevance to the input.



## How to use Gemini API

- First, you have to get an API key to use Gemini API.

- Click Create API key in existing project and select the project of GCP.


![API-keys](/GCP_pictures/AI/Google-AI-Studio/api-keys.PNG "API key creation")


- Once created, you will see a list of API keys generated below.

- You can then go ahead and grab the curl code beneath the list. Paste it into the project's cloud shell.


```
curl \
  -H 'Content-Type: application/json' \
  -d '{"contents":[{"parts":[{"text":"Write a story about a magic backpack"}]}]}' \
  -X POST https://generativelanguage.googleapis.com/v1beta/models/gemini-pro:generateContent?key=YOUR_API_KEY
```


- If this is working, then your API key is working.

- Then you can run some prompt in free form prompt and grab the code from the UI.


![grab-code](/GCP_pictures/AI/Google-AI-Studio/grab-code.PNG "Grab a code from the UI")


- Before you run your code on VM, first install the following:


```
pip install google-generativeai
```


- Also, be sure to change the API keys in the file. Then save the code as **gemini-request.py** file in the Cloud Shell editor. And run the file in the cloud shell by:

```
python gemini-request.py
```


![python-file-run](/GCP_pictures/AI/Google-AI-Studio/python-file-run.PNG "Run the python file in the cloud shell")


- You will see the response from the Gemini API in the cloud shell.


- Here is the example code that you use in the python file:


```

import google.generativeai as genai

genai.configure(api_key="your API keys")

# Set up the model
generation_config = {
  "temperature": 0.9,
  "top_p": 1,
  "top_k": 1,
  "max_output_tokens": 2048,
}

safety_settings = [
  {
    "category": "HARM_CATEGORY_HARASSMENT",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
  {
    "category": "HARM_CATEGORY_HATE_SPEECH",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
  {
    "category": "HARM_CATEGORY_SEXUALLY_EXPLICIT",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
  {
    "category": "HARM_CATEGORY_DANGEROUS_CONTENT",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
]

model = genai.GenerativeModel(model_name="gemini-pro",
                              generation_config=generation_config,
                              safety_settings=safety_settings)

prompt_parts = [
  "why do some people feel depressed?",
]

response = model.generate_content(prompt_parts)
print(response.text)
```


- To test the structured prompts using the Gemini API, first go to the Google AI Studio and click Structured Prompts. Run some prompt there and grab the code:


![structured-prompts-using-Gemini-API](/GCP_pictures/AI/Google-AI-Studio/gemini-api-for-structured-prompts.PNG "Test structured prompts using Gemini API")


- After taking the same steps as above for the free form prompt to be loaded onto your GCP VM, you can run the following:

```
python structured-prompts.py
```


![structured-prompts-cloud-shell](/GCP_pictures/AI/Google-AI-Studio/structrued-prompts-cloud-shell.PNG "Structured prompts run in the cloud shell")


- Here is the example structured prompt code in the python file:


```

import google.generativeai as genai

genai.configure(api_key="YOUR_API_KEY")

# Set up the model
generation_config = {
  "temperature": 0.9,
  "top_p": 1,
  "top_k": 1,
  "max_output_tokens": 2048,
}

safety_settings = [
  {
    "category": "HARM_CATEGORY_HARASSMENT",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
  {
    "category": "HARM_CATEGORY_HATE_SPEECH",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
  {
    "category": "HARM_CATEGORY_SEXUALLY_EXPLICIT",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
  {
    "category": "HARM_CATEGORY_DANGEROUS_CONTENT",
    "threshold": "BLOCK_MEDIUM_AND_ABOVE"
  },
]

model = genai.GenerativeModel(model_name="gemini-pro",
                              generation_config=generation_config,
                              safety_settings=safety_settings)

prompt_parts = [
  "input:Product Name Kaira Gold Lace-Up Heels",
  "output:Product Description Comfort and style can be yours with the Lulus Kaira Gold Lace-Up Heels! Metallic gold vegan leather shapes these single-sole heels with a slender toe strap, heel cup, and long laces that wrap and tie around the ankle. Gold aglets.",
  "input:Product Name Zelena Cherry Satin Patent Pointed-Toe Pumps",
  "output:Product Description The Lulus Zelena Cherry Satin Pointed-Toe Pumps are essential when you want to create a stand out look! Sleek woven satin leather shapes these statement-making heels that have a sophisticated pointed-toe upper with a low-cut collar, a slender slingback strap (with elastic at the side), and a quarter-style adjustable strap that secures with a shiny buckle. A ultra-trendy blade heel completes the stunning design!",
  "input:Product Name Brooklyn Light Pink Leather Pointed-Toe Slingback Pumps",
  "output:Product Description The Seychelles Brooklyn Light Pink Leather Pointed-Toe Slingback Pumps are an essential when it comes to creating an effortlessly sophisticated look! Smooth genuine leather shapes a classy pointed-toe upper that flows into a trendy slingback strap (with a bit of elastic at the side for fit). A sculpted kitten heel adds the perfect amount of height to this chic look!",
  "input:Product Name Buckled Pointed-Toe Flat Shoes",
  "output:Product Description ",
]

response = model.generate_content(prompt_parts)
print(response.text)
```


## How to get started with Vertiex AI

- Vertex AI Gemini API and Google AI Gemini API both let you incorporate the capabilities of Gemini models into your applications. 

- Vertex AI Gemini API is designed for developers and enterprises for use in scaled deployments.

- It offers features such as enterprise security, data residency, performance, and technical support. 

- If you are an **existing Google Cloud customer** or deploy medium to large scale applications you are in the right place.

- If you are a hobbyist, student, or developer who is new to Google Cloud, try the Google AI Gemini API, which is suitable for experimentation, prototyping, and small deployments. 

- If you are looking for a way to use Gemini directly from your mobile and web apps, see the Google AI SDKs for Android, Swift, and web.



 ### How to use Vertex AI 

  - Go to Vertex AI on GCP and click Language on the left side bar.


  ![vertext-ai-interface](/GCP_pictures/AI/Google-AI-Studio/start-vertexai.PNG "Start Vertext AI")



  - And this takes me to the Gemini Pro like below. It has the similar prompt interface and settings options as Google AI studio:


  ![gemini-pro-gcp](/GCP_pictures/AI/Google-AI-Studio/gemini-pro-gcp.PNG "How to use Gemini Pro on GCP")


  - Click Get Code and you can see the code structure of Vertex AI Gemini Pro model.


  ![vertex-ai-code](/GCP_pictures/AI/Google-AI-Studio/vertex-ai-code.PNG "Vertex AI code")


  - One of the beneficial features of Vertex AI is that it supports Multimodal including video prompts and responses. Insert a video and ask what this is about. One caveat is that it can sometimes extrapolate beyond what's actually in the video:


  ![multimodal-video-prompt](/GCP_pictures/AI/Google-AI-Studio/multimodal-video-prompt.PNG "Multimodal video prompt")




 