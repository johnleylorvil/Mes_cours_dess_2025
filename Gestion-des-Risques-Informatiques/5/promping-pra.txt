import requests
# Lire votre base de connaissances
with open("/home/austin/miniconda3/pca1.txt", "r", encoding="utf-8") as f:
    base_connaissance = f.read()
question = input("")
prompt = f"Voici un extrait de ma base de connaissance : {base_connaissance} À partir de ces informations réponds à la question suivante :{question}"
def demander_mixtral(prompt):
    response = requests.post("http://localhost:11434/api/generate",json={"model": "mistral","prompt": prompt,"stream":False})
    return response
reponse = demander_mixtral(prompt)
if reponse.status_code == 200:
    result = reponse.json()
    print("Réponse du modèle :", result["response"])
else:
    print("Erreur :", reponse.status_code, reponse.text)