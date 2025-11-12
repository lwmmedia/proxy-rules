# Guide d'utilisation des Subscriptions dans Stash

## 📌 Qu'est-ce qu'une URL de subscription ?

Une **URL de subscription** est un lien fourni par votre **fournisseur de proxy/VPN** qui contient :
- 🖥️ Les serveurs proxy (Shadowsocks, V2Ray, Trojan, etc.)
- 📊 Informations de quota (trafic utilisé/restant)
- 📅 Date d'expiration de l'abonnement
- 🔄 Mise à jour automatique de la configuration

## ⚠️ Important

**Le dépôt proxy-rules ne fournit PAS de serveurs proxy !**

Ce dépôt contient uniquement des **règles de routage**. Pour utiliser une subscription URL, vous devez :
1. Avoir un abonnement chez un fournisseur de proxy/VPN
2. Obtenir votre URL de subscription de ce fournisseur
3. L'ajouter à la configuration Stash

---

## 🔧 Configuration dans Stash

### Méthode 1 : Subscription URL simple (affichage des infos uniquement)

Dans le fichier `complete.yaml`, ligne 9, décommentez et remplissez :

```yaml
# Subscription Configuration
subscribe-url: "https://your-provider.com/api/v1/client/subscribe?token=YOUR-TOKEN"
```

**Fonction :** Affiche le trafic et la date d'expiration dans l'interface Stash

---

### Méthode 2 : Proxy Provider (chargement automatique des serveurs)

Dans la section `proxy-providers` (ligne 100), décommentez et configurez :

```yaml
proxy-providers:
  my-provider:
    type: http
    url: "https://your-provider.com/api/v1/client/subscribe?token=YOUR-TOKEN"
    interval: 3600  # Mise à jour toutes les heures
    path: ./providers/my-provider.yaml
    health-check:
      enable: true
      interval: 600  # Vérification de santé toutes les 10 minutes
      url: http://www.google.com/generate_204
```

Puis dans le groupe `Auto` (ligne 160), décommentez :

```yaml
  - name: Auto
    type: url-test
    url: http://www.google.com/generate_204
    interval: 300
    tolerance: 50
    use:
      - my-provider  # Utilise tous les proxies du provider
```

**Fonction :** Charge automatiquement tous les serveurs depuis l'URL et les teste

---

## 📋 Exemples de fournisseurs populaires

### Format d'URL typique :

```
https://sub.provider.com/link/ABCD1234?mu=1
https://api.provider.com/api/v1/client/subscribe?token=abc123xyz
https://provider.com/sub?target=clash&token=your-token
```

### Fournisseurs français/européens courants :
- **Mullvad VPN** (Suède)
- **ProtonVPN** (Suisse)
- **NordVPN**
- **Surfshark**
- Services personnels (VPS auto-hébergés)

---

## 🔐 Sécurité

⚠️ **Votre URL de subscription contient des informations sensibles !**

- ❌ Ne partagez JAMAIS votre URL
- ❌ Ne la publiez pas publiquement
- ✅ Gardez-la confidentielle
- ✅ Changez le token si vous pensez qu'elle a été compromise

---

## 🎯 Scénarios d'utilisation

### Scénario A : Vous avez un abonnement VPN avec subscription URL

1. Obtenez l'URL de votre fournisseur
2. Ajoutez-la dans `subscribe-url` OU `proxy-providers`
3. Stash chargera automatiquement les serveurs et affichera votre quota

### Scénario B : Vous n'avez pas de fournisseur

Les configurations de ce dépôt fonctionnent avec :
- Des serveurs gratuits (trouvés sur GitHub/Telegram)
- Votre propre VPS avec Shadowsocks/V2Ray installé
- Configuration manuelle dans la section `proxies:`

### Scénario C : Vous voulez juste les règles de routage

Utilisez les fichiers tels quels et ajoutez vos proxies manuellement dans la section `proxies:` (ligne 112+).

---

## 📞 Support

Pour obtenir votre URL de subscription, contactez **votre fournisseur de proxy/VPN**.

Ce dépôt (proxy-rules) fournit uniquement :
- ✅ Règles de routage intelligentes
- ✅ Configurations optimisées pour la France
- ✅ Templates prêts à l'emploi
- ❌ Pas de serveurs proxy
- ❌ Pas d'URL de subscription

---

## 🔗 Ressources

- [Documentation Stash](https://stash.wiki/)
- [Format Clash](https://github.com/Dreamacro/clash/wiki/configuration)
- [Proxy Providers](https://stash.wiki/features/proxy-providers)

---

**Dernière mise à jour :** Novembre 2025
