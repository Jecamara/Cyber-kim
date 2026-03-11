# Cyber-kim
Gestion ticket cyber

Upload login.html + cyber-kim-logo.svg dans flash/hotspot/ via Winbox → Files
Colle les commandes de profils dans le terminal MikroTik
Teste depuis un téléphone client

Génération de jeton disponible sur https://jecamara.github.io/Cyber-kim/cyber-kim-jetons.html
******
Architecture simplifiée
PC Gérant (navigateur)
        │
        ▼
App Cyber Kim (HTML local)
        │
        │ API REST (port 8728/80)
        ▼
MikroTik HAP AC2
   └── Sessions actives
   └── Jetons utilisés
   └── Statistiques trafic

⚙️ ÉTAPE 1 — Activer l'API REST sur MikroTik
Dans Winbox → Terminal :
bash# Activer l'API REST (port 80)
/ip service enable www
/ip service set www port=80

# Activer l'API sur port 8728
/ip service enable api
/ip service set api port=8728

# Créer un user dédié dashboard (lecture seule)
/user add name=dashboard \
  password=CyberKim2025 \
  group=read
```
Active l'API REST sur MikroTik (Winbox → Terminal) :

bash/ip service enable www
/ip service set www port=80
/user add name=dashboard password=TonMotDePasse group=read

Dans l'app → onglet 🔴 Live → entre l'IP + identifiants → Connecter
Actualisation automatique toutes les 10 secondes 🔄

---

## ⚙️ ÉTAPE 2 — Tester l'API depuis le navigateur

Ouvre ce lien sur le PC connecté au MikroTik :
```
http://192.168.17.1/rest/ip/hotspot/active
Si tu vois du JSON → l'API fonctionne ✅
