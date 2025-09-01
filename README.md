# Proxy Rules Collection

Custom rule sets for iOS proxy applications: **Loon**, **Shadowrocket**, and **Stash**.

## 🚀 Quick Start

### Loon

```ini
[Rule]
RULE-SET,https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/streaming/youtube.list,YouTube,tag=YouTube,enabled=true
RULE-SET,https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/streaming/netflix.list,Netflix,tag=Netflix,enabled=true
```

### Shadowrocket

```ini
[Rule]
RULE-SET,https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/streaming/youtube.list,YouTube
RULE-SET,https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/streaming/netflix.list,Netflix
```

### Stash

```yaml
rule-providers:
  YouTube:
    type: http
    behavior: classical
    url: https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/streaming/youtube.list
    interval: 86400

rules:
  - RULE-SET,YouTube,YouTube
```

## 📁 Available Rules

### Streaming Services

|Service|Rule File                     |Description                       |
|-------|------------------------------|----------------------------------|
|YouTube|`rules/streaming/youtube.list`|YouTube, YouTube Music, YouTube TV|
|Netflix|`rules/streaming/netflix.list`|Netflix global domains            |
|Twitch |`rules/streaming/twitch.list` |Twitch streaming platform         |
|Spotify|`rules/streaming/spotify.list`|Spotify music streaming           |
|Disney+|`rules/streaming/disney.list` |Disney Plus streaming             |

### Social Media

|Service  |Rule File                    |Description              |
|---------|-----------------------------|-------------------------|
|Telegram |`rules/social/telegram.list` |Telegram messaging       |
|Discord  |`rules/social/discord.list`  |Discord voice/text chat  |
|Twitter/X|`rules/social/twitter.list`  |Twitter/X social platform|
|Instagram|`rules/social/instagram.list`|Instagram social media   |

### Global Services

|Service  |Rule File                    |Description                           |
|---------|-----------------------------|--------------------------------------|
|Google   |`rules/global/google.list`   |Google services (Search, Gmail, Drive)|
|Microsoft|`rules/global/microsoft.list`|Microsoft 365, Azure, Xbox            |
|Apple    |`rules/global/apple.list`    |Apple services (iCloud, App Store)    |
|OpenAI   |`rules/global/openai.list`   |ChatGPT, OpenAI API                   |

### Regional Rules

|Region      |Rule File                |Description                          |
|------------|-------------------------|-------------------------------------|
|China Direct|`rules/china/direct.list`|Chinese domains for direct connection|
|China Block |`rules/china/reject.list`|Domains to block in China            |

## 🔗 Raw URLs

Direct URLs ready to use:

```
https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/streaming/youtube.list
https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/streaming/netflix.list
https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/social/telegram.list
https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/global/google.list
```

## 📋 Complete Configuration Examples

### Loon Full Configuration

```ini
[General]
ipv6 = false
skip-proxy = 192.168.0.0/16,10.0.0.0/8,172.16.0.0/12,localhost,*.local
dns-server = 223.5.5.5,114.114.114.114

[Proxy]
# Add your proxy servers here

[Proxy Group]
YouTube = select,Auto,HK,US,SG,interval=300,timeout=3
Netflix = select,Auto,US,UK,JP,interval=300,timeout=3
Global = select,Auto,HK,US,SG,interval=300,timeout=3
Telegram = select,Auto,HK,SG,US,interval=300,timeout=3

[Rule]
RULE-SET,https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/streaming/youtube.list,YouTube,tag=YouTube,enabled=true
RULE-SET,https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/streaming/netflix.list,Netflix,tag=Netflix,enabled=true
RULE-SET,https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/social/telegram.list,Telegram,tag=Telegram,enabled=true
RULE-SET,https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/global/google.list,Global,tag=Global,enabled=true

GEOIP,CN,DIRECT
FINAL,Global
```

### Shadowrocket Configuration

```ini
[General]
bypass-system = true
skip-proxy = 192.168.0.0/16,10.0.0.0/8,172.16.0.0/12,localhost,*.local,captive.apple.com
dns-server = 223.5.5.5, 114.114.114.114

[Rule]
RULE-SET,https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/streaming/youtube.list,YouTube
RULE-SET,https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/streaming/netflix.list,Netflix
RULE-SET,https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/social/telegram.list,Telegram
RULE-SET,https://raw.githubusercontent.com/lwmmedia/proxy-rules/main/rules/global/google.list,Global

GEOIP,CN,DIRECT
FINAL,PROXY
```

## 🛠️ Rule Format

Rules follow standard proxy app format:

```
# Comments start with #
DOMAIN-SUFFIX,example.com          # Matches example.com and all subdomains
DOMAIN-KEYWORD,example             # Matches domains containing "example"
DOMAIN,exact.example.com           # Matches exact domain only
IP-CIDR,192.168.1.0/24            # Matches IP range
USER-AGENT,*App*                   # Matches user agent containing "App"
```

## 📊 Update Schedule

- **Manual Updates**: As needed for new services or domain changes
- **Automated Updates**: GitHub Actions can be configured for daily updates
- **Community Updates**: Pull requests welcome for additions and corrections

## 📝 Usage Tips

1. **Start Simple**: Begin with YouTube and Google rules
1. **Test Configuration**: Verify rules work in your environment
1. **Monitor Performance**: Some rules may impact connection speed
1. **Regular Updates**: Check for new domains and services periodically

## 🤝 Contributing

### Adding New Rules

1. Fork the repository
1. Create rule file in appropriate category
1. Test the rules
1. Submit pull request

### Rule Categories

- `/rules/streaming/` - Video/audio streaming services
- `/rules/social/` - Social media platforms
- `/rules/global/` - International tech companies
- `/rules/china/` - China-specific routing rules
- `/rules/gaming/` - Gaming platforms and services

### Quality Guidelines

- Use official domain names only
- Test rules before submitting
- Include service description in comments
- Follow existing file naming convention

## 📞 Support

- **Issues**: Report problems via GitHub Issues
- **Feature Requests**: Use GitHub Issues with enhancement label
- **Questions**: Check existing issues or create new one

## 📜 License

MIT License - Feel free to fork and customize for your needs.

## ⚠️ Disclaimer

These rules are for educational and personal use. Ensure compliance with local laws and service terms. Proxy usage may violate some service agreements.

-----

**Last Updated**: 2025-01-15  
**Maintained by**: [Your Name]  
**Repository**: https://github.com/lwmmedia/proxy-rules
