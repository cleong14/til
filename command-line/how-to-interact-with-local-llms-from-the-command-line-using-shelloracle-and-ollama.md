# 2024-03-11 - TIL - How to Interact with Local LLMs from the Command-Line Using ShellOracle and Ollama

ShellOracle is an innovative terminal utility designed for intelligent shell command generation. ShellOracle currently supports Ollama, LocalAI, and OpenAI.

Ollama allows users to "get up and running with large language models locally".


## Usage

```sh
### install/start ollama and pull a model from a registry
# install ollama
brew install ollama
# start ollama
ollama serve
# pull a model from a registry
ollama pull zephyr

### install/configure shelloracle with ollama as a provider
# pip install shelloracle
python3 -m pip install shelloracle
# configure shelloracle with ollama as a provider
python3 -m shelloracle configure

### run shelloracle
## option 1 - keybinding then describe your command
# 1. press `CTRL+F`
# 2. describe your command
# 3. press `Enter`
## option 2 - chain/pipe other commands to shelloracle
echo "find all json files in the cwd" | shor
> `find . -type f -name '*.json'` # shelloracle generated command output
```


## Use Cases

- Interact with local LLMs from the command-line
- Reduce the amount of context/app switching needed when using other LLMs (e.g. Web UIs)


## References

- [djcopley/ShellOracle: A terminal utility for intelligent shell command generation](https://github.com/djcopley/ShellOracle)
- [ollama/ollama: Get up and running with Llama 2, Mistral, Gemma, and other large language models.](https://github.com/ollama/ollama)

