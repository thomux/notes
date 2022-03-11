# Additional plugins

https://github.com/zsh-users/zsh-syntax-highlighting

https://github.com/zsh-users/zsh-autosuggestions

# Additional tools

apt install python3-pygments 

# Config

ZSH_THEME="robbyrussell"

plugins=(
	git
	command-not-found
	colorize
	common-aliases
	python
	vscode
	golang
	zsh-autosuggestions
	zsh-syntax-highlighting
)

export PATH=~/bin/:$PATH

alias cl="pygmentize -O style=stata-dark -l python -s | less -R"
