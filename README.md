import requests
from bs4 import BeautifulSoup
import discord
import asyncio

# Replace with your Discord webhook URL
DISCORD_WEBHOOK_URL = "https://discord.com/api/webhooks/1156275318752018502/yGRiBuw1brhH1QDSQWe6P45pPNPY0-3xqpYg9u8VI5D1EhqDk6c7QHRM1Q63sOoOlP6z"

# The URL of the website you want to monitor
WEBSITE_URL = "https://www.pokeguardian.com/sets/upcoming-sets"

# Initialize a Discord client
client = discord.Webhook.from_url(DISCORD_WEBHOOK_URL, adapter=discord.RequestsWebhookAdapter())

# Store the initial content of the website
initial_content = "https://www.pokeguardian.com/sets/upcoming-sets"

# Function to fetch the website content
async def fetch_website_content():
    global initial_content
    while True:
        try:
            # Send a GET request to the website
            response = requests.get(WEBSITE_URL)
            response.raise_for_status()

 # Parse the HTML content of the page
 soup = BeautifulSoup(response.text, "html.parser")

# Extract the main content of the page that you want to monitor
content = str(soup.find("div", class_="jw-element-imagetext-text"))

# Check if the content has changed
 if content != initial_content:
                # Content has changed, send a notification to Discord
                await client.send(content="New Update to site:\n" + WEBSITE_URL)
                initial_content = content

 except Exception as e:
            print("Error:", str(e))

  # Wait for a specified interval before checking again (e.g., 1 hour)
 await asyncio.sleep(3600)

# Run the monitoring function
if __name__ == "__main__":
    loop = asyncio.get_event_loop()
    loop.run_until_complete(fetch_website_content())
