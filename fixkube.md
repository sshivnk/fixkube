fixkube

##fixkube is a small Python-powered command-line tool that helps you debug Kubernetes / kubectl errors using a local Ollama LLM model.

Instead of manually searching for cryptic kubectl error messages, you can simply:

kubectl get pods -n xyz 2>&1 | fixkube


or

fixkube "error: the server doesn't have a resource type 'ingresses'"


fixkube will connect to your local Ollama model, analyze the error, explain the likely cause, and provide actionable steps to fix it.

🚀 Features

Debug kubectl errors instantly using local LLM

Works in two modes:

Pipe mode (recommended)

Direct text mode

Automatically fetches:

kubectl version

current context

current namespace

Provides:

Explanation of the error

Root cause

Suggested kubectl commands and next steps

Zero cloud dependency → fully local

Fast and lightweight

🛠️ Requirements

Python 3

Ollama installed and running

A local LLM pulled, for example:

ollama pull llama3.1

📦 Installation

Save the script below as fixkube (no extension):


Make it executable:

~~~
chmod +x fixkube
~~~

Add it to your PATH:

mkdir -p ~/bin
mv fixkube ~/bin/
echo 'export PATH="$HOME/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc

🧪 Usage
1. Pipe kubectl error (recommended)
kubectl get pods -n xyz 2>&1 | fixkube

2. Pass manual error text
fixkube "error: the server doesn't have a resource type 'ingresses'"

3. Fix invalid YAML or apply issues
kubectl apply -f bad.yaml 2>&1 | fixkube

🧠 How It Works

Reads kubectl error from:

stdin

OR command-line arguments

Gathers your current Kubernetes context

Builds a structured prompt for the LLM

Sends it to Ollama running locally

Prints a clean, actionable diagnosis

🛡️ Why Local?

No cloud API calls

No data leaves your machine

Instant response time

Free (you run your own model)

📌 Roadmap

fixkube kubectl ... mode

Support for multiple models

--explain and --verbose flags

Rich formatting output

Packaging as pip module (pip install fixkube)
