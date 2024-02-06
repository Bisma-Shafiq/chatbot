# chatbot
import csv
import nltk
from nltk.chat.util import Chat, reflections

def load_dataset(csv_file):
    patterns = []
    responses = []
    
    with open(csv_file, 'r') as file:
        reader = csv.reader(file)
        for row in reader:
            if len(row) == 2:
                patterns.append(row[0])
                responses.append(row[1])
    
    return list(zip(patterns, responses))

# Load dataset from CSV file
csv_file_path = 'your_dataset.csv'  # Provide the path to your CSV file
dataset = load_dataset(csv_file_path)

# Create patterns and responses from the loaded dataset
patterns, responses = zip(*dataset)

# Define chatbot using the loaded dataset
chatbot = Chat(list(zip(patterns, responses)), reflections)

# Function to start the conversation with the chatbot
def start_chat():
    print("Hello! I'm ChatBot. Type 'bye' to exit.")
    while True:
        user_input = input("You: ")
        if user_input.lower() == 'bye':
            print("ChatBot: Goodbye!")
            break
        response = chatbot.respond(user_input)
        print("ChatBot:", response)

# Start the conversation
if __name__ == "__main__":
    start_chat()
