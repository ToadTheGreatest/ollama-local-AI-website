# ollama-local-AI-website
This frontend website uses local AI models instead of data centers


Supports model interchanging and custom models you create. Does not set system prompt so you can use custom system prompted models you make to make interactions more customizeable.

[Use it now](https://toadthegreatest.github.io/ollama-local-AI-website)
*note: you may have to tell ollama to allow github pages to access the server running on your machine, OR you can just download index.html and run that in a local server.*

***

# How to use

## 1. Install Ollama

There are three ways to install ollama.

### The first way: 

[Follow the official instructions](https://github.com/Ollama/ollama#readme)

if you do so, jump [here](#2-run-olama)

### The second way:

Download via shell command

#### Windows
```powershell
irm https://ollama.com/install.ps1 | iex
```

#### Mac / Linux
```bash
curl -fsSL https://ollama.com/install.sh | sh
```

### The third way

Download the installer (these download automatically)

Windows users, click [here](https://ollama.com/download/OllamaSetup.exe) and run it. This is the installer

Mac users,  click [here](https://ollama.com/download/Ollama.dmg) and install it.

Linux users, go [here](#the-second-way) or [here](#the-first-way)

## 2. Run olama

```bash
ollama
```

this should give you a welcome screen in the terminal.

## 3. Edit Ollama Settings

### Windows users

Go into your system settings and search for Environment Variables and click Edit Environment Variables For Your Account

A window should pop up, in the middle, click Add

Then in the top text box in the window that appears, type `OLLAMA_ORIGINS`

In the bottom type `*`

Restart ollama from your system tray.

### Mac users

Type in the following command
```bash
launchctl setenv OLLAMA_ORIGINS "*"
```

Restart ollama with the menu bar then relaunch in your apps

### Linux users:

```bash
sudo systemctl edit ollama.service
```

add the following to the text file in the editor that opens

```text
[Service]
Environment="OLLAMA_ORIGINS=*"
```

Exit the text editor. If it does not save and you get a message in the terminal, there is another way.

type the following command
```bash
sudo mkdir -p /etc/systemd/system/ollama.service.d && printf "[Service]\nEnvironment=\"OLLAMA_ORIGINS=*\"\n" | sudo tee /etc/systemd/system/ollama.service.d/override.conf > /dev/null && sudo systemctl daemon-reload
```

or the following multiple commands
```bash
sudo mkdir -p /etc/systemd/system/ollama.service.d
printf "[Service]\nEnvironment=\"OLLAMA_ORIGINS=*\"\n" | sudo tee /etc/systemd/system/ollama.service.d/override.conf > /dev/null
sudo systemctl daemon-reload
```

restart ollama with the following command

```bash
sudo systemctl restart ollama
```

## 4. Use the website

This should have ollama set up so the website can acess it. Click (here)[https://toadthegreatest.github.io/ollama-local-AI-website].

To install more models, in the website, select [install model] in the model selector dropdown and in the prompt, type the name of the model.

You can get model names from the (official ollama website)[https://ollama.com/models]. Search for the model and then you can use this tool to turn the model name into a model ID.
<html>
<body>
<label>Model Name: </label>
<input type="text" id="model-name"><br>
<label>Parameters: </label>
<input type="number" id="parameters">
<select id="num-param-unit">
<option value="m">Million</option>
<option value="b" selected>Billion</option>
<option value="t">Trillion</option>
</select>
<span>Parameters</span>
<br>
<br>
<span style="background-color:#333;border-color:#333;border-radius:5px" id="model-id"><span>
<script>
    function get_model_id() {
        const name = document.getElementById("model-name").value;
        const params = document.getElementById("parameters").value;
        const p_unit = document.getElementById("num-param-unit").value;
        const output = document.getElementById("model-id");
        if (name.trim().replace(" ", "-") && params && p_unit) {
            var modelid = `${name.trim().replace("-","").toLowerCase()}:${params}${p_unit}`;
            output.textContent = modelid;
        }
    }
    document.getElementById("model-name").addEventListener("input", get_model_id);
    document.getElementById("parameters").addEventListener("input", get_model_id);
    document.getElementById("num-param-unit").addEventListener("input", get_model_id);
</script>
</body>
</html>