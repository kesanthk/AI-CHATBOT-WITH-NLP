# AI-CHATBOT-WITH-NLP
import nltk
from nltk.chat.util import Chat, reflections
import random

# Download necessary NLTK data (run this once)
try:
    nltk.data.find('corpora/wordnet')
except nltk.downloader.DownloadError:
    nltk.download('punkt')
    nltk.download('wordnet')
    nltk.download('averaged_perceptron_tagger')
    nltk.download('stopwords')


# Define patterns and responses
# Each tuple contains: (pattern_regex, [list_of_responses])
patterns = [
    (r'hi|hello|hey', ['Hello!', 'Hi there!', 'Hey!', 'Greetings!']),
    (r'how are you\?', ["I'm doing well, thank you!", "I'm a bot, but I'm functioning perfectly!", "All good! How about you?"]),
    (r'what is your name\?', ["You can call me ChatBot.", "I don't have a name, I'm just a program.", "I'm your friendly neighborhood ChatBot!"]),
    (r'what can you do\?', ["I can answer basic questions and chat with you.", "I can respond to your queries and engage in simple conversations."]),
    (r'who created you\?', ["I was created by a developer using Python.", "A programmer brought me to life."]),
    (r'bye|goodbye|see you', ['Goodbye!', 'See you later!', 'Bye for now!', 'It was nice chatting!']),
    (r'(.*) your age\?', ["I don't have an age, I'm a computer program.", "Age is just a number, and I don't have one!"]),
    (r'(.*) (weather|temperature) in (.*)', ["I can't tell you the current weather, as I don't have access to real-time weather data.", "I'm not equipped to provide weather forecasts."]),
    (r'(.*) help (.*)', ["I'm here to assist you. What do you need help with?", "Tell me how I can help you."]),
    (r'thanks|thank you', ["You're welcome!", "No problem!", "Glad I could help!"]),
    (r'.*', ["I'm sorry, I don't understand that.", "Could you please rephrase your question?", "I'm still learning, please try another query."])
]

# Reflections are used to transform first-person phrases to second-person and vice-versa.
# For example, "I am" becomes "you are" in the response.
reflections = {
    "i am": "you are",
    "i was": "you were",
    "i": "you",
    "i'm": "you're",
    "my": "your",
    "you are": "I am",
    "you were": "I was",
    "you": "I",
    "you're": "I'm",
    "your": "my",
    "me": "you"
}

# Create the chatbot
chatbot = Chat(patterns, reflections)

def start_chatbot():
    print("Welcome! I'm a simple chatbot. Type 'quit' or 'bye' to exit.")
    while True:
        user_input = input("You: ")
        if user_input.lower() in ['quit', 'bye', 'goodbye']:
            print("ChatBot: Goodbye! Have a great day!")
            break
        response = chatbot.respond(user_input)
        if response:
            print("ChatBot:", response)
        else:
            # Fallback if no pattern matches (should be covered by the last pattern but good to have)
            print("ChatBot: I'm not sure how to respond to that. Can you ask something else?")

if __name__ == "__main__":
    start_chatbot()
