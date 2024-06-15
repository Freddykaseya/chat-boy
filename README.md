# chat-boy
import tkinter as tk
from tkinter import scrolledtext
import random

# Fonction pour gérer les réponses aux salutations
def repondre_salutation():
    reponses = [
        "Bonjour! Comment puis-je vous aider aujourd'hui ?",
        "Salut! Que puis-je faire pour vous ?",
        "Bonjour! En quoi puis-je vous être utile ?",
        "Hello! Comment puis-je vous assister ?"
    ]
    return random.choice(reponses)

# Fonction pour gérer les réponses aux questions spécifiques
def repondre_question(question):
    question = question.lower().strip()
    
    if "comment ça va" in question:
        return "Ça va bien, merci!"
    elif "quel est ton nom" in question:
        return "Je suis un assistant virtuel de Freddy Kaseya!"
    elif "quelle est ta ville" in question or "quel est ta ville" in question:
        return "Je viens de L'shi"
    elif "l'shi c'est quoi" in question:
        return "L'shi ni NSUPU"
    elif "quelle est ta nourriture préférée" in question or "quel est ta nourriture préférée" in question:
        return "BUKARI NA SOMBE"
    elif "merci" in question:
        return "AKUNA MATATA"
    elif "bye" in question:
        return "LAMBA LIA TO KO YA TE"
    else:
        return "Désolé, je ne suis pas sûr de comprendre. Pouvez-vous reformuler votre question ?"

# Fonction pour envoyer le message
def envoyer_message():
    user_input = input_box.get("1.0", tk.END).strip()
    if not user_input:
        return
    
    chat_box.config(state=tk.NORMAL)
    chat_box.insert(tk.END, f"Vous: {user_input}\n")
    
    # Vérification si l'utilisateur dit bonjour
    if any(greeting_word in user_input.lower() for greeting_word in ["bonjour", "salut", "hello", "coucou", "hey"]):
        response = repondre_salutation()
    # Vérification si l'utilisateur pose une question
    elif any(question_word in user_input.lower() for question_word in ["comment ça va", "quel est ton nom", "quelle est ta ville", "quel est ta ville", "l'shi c'est quoi", "quelle est ta nourriture préférée", "quel est ta nourriture préférée", "merci"]):
        response = repondre_question(user_input)
    # Condition pour quitter le programme
    elif "au revoir" in user_input.lower():
        response = "Au revoir!"
    else:
        response = "Désolé, je ne comprends pas. Pouvez-vous reformuler ?"
    
    chat_box.insert(tk.END, f"Assistant: {response}\n")
    chat_box.config(state=tk.DISABLED)
    
    input_box.delete("1.0", tk.END)

# Créer la fenêtre principale
root = tk.Tk()
root.title("Assistant Virtuel")

# Créer la zone de texte pour afficher la conversation
chat_box = scrolledtext.ScrolledText(root, state='disabled', wrap=tk.WORD, width=60, height=20)
chat_box.grid(row=0, column=0, columnspan=2, padx=10, pady=10)

# Créer la zone de saisie pour entrer le message
input_box = tk.Text(root, height=2, width=48)
input_box.grid(row=1, column=0, padx=10, pady=10)

# Créer le bouton pour envoyer le message
send_button = tk.Button(root, text="Envoyer", command=envoyer_message)
send_button.grid(row=1, column=1, padx=10, pady=10)

# Démarrer la boucle principale
root.mainloop()
