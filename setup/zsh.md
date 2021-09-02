# ZSH AND OH MY ZSH INSTALLATION

&nbsp;

## Step 01. Install zsh

```shell
sudo apt-get install zsh
```

After installing, we might make zsh the default shell:

```shell
sudo chsh -s $(which zsh)
```

Note: Restart (or logout) to take effects.

&nbsp;

## Step 02. Install oh-my-zsh

Follow instructions from this url:

<https://github.com/ohmyzsh/ohmyzsh>

&nbsp;

## Step 03. Install powerlevel10k theme

Note: Theme directory location: ```~/.oh-my-zsh/custom/themes```.

Clone repo into theme directory location: <https://github.com/romkatv/powerlevel10k>.

After cloning, add this line into ```~/.zshrc```:

```text
source ~/.oh-my-zsh/custom/themes/powerlevel10k/powerlevel10k.zsh-theme
```

Note: This line must below the line ```source $ZSH/oh-my-zsh.sh```.

&nbsp;

## Step 04. Install plugins

Note: Plugin directory location: ```~/.oh-my-zsh/custom/plugins```.

### List of plugins

#### zsh-autosuggestions

<https://github.com/zsh-users/zsh-autosuggestions>

#### zsh-syntax-highlighting

<https://github.com/zsh-users/zsh-syntax-highlighting>

Note that you should not add line ```source ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh``` into ```~/.zshrc```.

### Notes

Final plugin line in ```~/.zshrc```:

```text
plugins=(git z zsh-autosuggestions zsh-syntax-highlighting)
```
