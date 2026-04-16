
# Qwen CLI + OpenRouter Setup Guide (Windows 10)

**Last updated:** April 2026  
**Goal:** Use free OpenRouter models (`google/gemma-4-31b-it:free` and `qwen/qwen3-coder:free`) in Qwen CLI

### 1. Create the `.env` file (stores your API key safely)

1. Open File Explorer → go to:  
   `C:\Users\Mozdalif\.qwen`
2. Create a new file named **`.env`** (note the dot at the beginning).
3. Paste exactly this inside it:

```dotenv
OPENROUTER_API_KEY=sk-or-v1-XXXXXXXXXXXXXXXXXXXXXXXX
```

Replace `sk-or-v1-XXXXXXXXXXXXXXXXXXXXXXXX` with your real OpenRouter API key.  
Save the file.

### 2. Create/Edit the main `settings.json` (user-level)

1. Press `Win + R`, paste this and press Enter:  
   `%USERPROFILE%\.qwen\settings.json`
2. Replace **everything** with the following:

```json
{
  "security": {
    "auth": {
      "selectedType": "openai"
    }
  },
  "ui": {
    "theme": "ANSI"
  },
  "modelProviders": {
    "openai": [
      {
        "id": "google/gemma-4-31b-it:free",
        "name": "Gemma 4 31B IT (Free via OpenRouter)",
        "envKey": "OPENROUTER_API_KEY",
        "baseUrl": "https://openrouter.ai/api/v1",
        "generationConfig": {
          "timeout": 120000,
          "maxRetries": 3,
          "samplingParams": {
            "temperature": 0.7,
            "max_tokens": 4096
          }
        }
      },
      {
        "id": "qwen/qwen3-coder:free",
        "name": "Qwen3 Coder (Free via OpenRouter)",
        "envKey": "OPENROUTER_API_KEY",
        "baseUrl": "https://openrouter.ai/api/v1",
        "generationConfig": {
          "timeout": 120000,
          "maxRetries": 3,
          "samplingParams": {
            "temperature": 0.7,
            "max_tokens": 8192
          }
        }
      }
    ]
  },
  "$version": 3
}
```

Save the file.

### 3. First-time run & Authentication screens (important!)

1. Open Command Prompt / PowerShell / Terminal.
2. Type:
   ```bash
   qwen
   ```
3. When you see **“Select Authentication Method”**:
   - Arrow down to **API Key** → press **Enter**
4. When you see **“Select API Key Type”**:
   - Arrow down to **Custom API Key** → press **Enter**
5. When you see the **“Custom Configuration”** screen:
   - Press **Esc** key

You should now be in the normal chat.

### 4. Select your model

Inside the Qwen chat, type:
```
/model
```
You will see:
- Gemma 4 31B IT (Free via OpenRouter)
- Qwen3 Coder (Free via OpenRouter)

Choose the one you want and press Enter.

### 5. Quick start commands (recommended)

```bash
# Start directly with Gemma 4
qwen --model google/gemma-4-31b-it:free

# Start directly with Qwen3 Coder
qwen --model qwen/qwen3-coder:free
```

### 6. Troubleshooting: settings.json keeps resetting

If `qwen` resets your settings:
1. Go to your current project folder, for example:  
   `C:\Users\Mozdalif\Desktop\udemy_saver_all\python_youtube_saver`
2. Show hidden items (`View` → check **Hidden items**).
3. Delete the entire `.qwen` folder (or the `settings.json` inside it).
4. Run `qwen` again — it will now use the correct user-level settings.

### 7. Adding more OpenRouter models later

Just add another object inside the `"openai": [ ... ]` array in `settings.json` using the same format.

Example model IDs you can copy:
- `anthropic/claude-3-5-sonnet`
- `openai/gpt-4o-mini`
- `deepseek/deepseek-r1:free`

---
