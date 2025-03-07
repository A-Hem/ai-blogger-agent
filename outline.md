import openai
import requests

# Set up OpenAI API key
openai.api_key = 'your_openai_api_key'

# Define your topic and prompt
topic = "Artificial Intelligence in Healthcare"
prompt = f"Write a detailed blog post about {topic}."

# Generate content using GPT-3
response = openai.Completion.create(
  engine="davinci-codex",
  prompt=prompt,
  max_tokens=500
)

# Get the generated text
generated_content = response.choices[0].text.strip()

# Define your blog API endpoint and authentication
blog_api_endpoint = "https://yourblogplatform.com/api/posts"
headers = {
    "Authorization": "Bearer your_blog_api_token",
    "Content-Type": "application/json"
}

# Create the blog post payload
blog_post_payload = {
    "title": topic,
    "content": generated_content,
    "status": "published"
}

# Publish the blog post
response = requests.post(blog_api_endpoint, headers=headers, json=blog_post_payload)

if response.status_code == 201:
    print("Blog post published successfully!")
else:
    print("Failed to publish blog post:", response.status_code, response.text)
