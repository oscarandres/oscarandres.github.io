1. Install Go:
```console
brew install go
```
2. Install nvim
```console
brew install neovim
```
3. Install vim-plug
```console
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
git clone https://github.com/fatih/vim-go.git ~/.vim/plugged/vim-go
```
4. Install vim-go and set autowrite:
- Add plug to neovim config (~/.config/nvim/init.vim):
```console
set autowrite

call plug#begin()
Plug 'fatih/vim-go', { 'do': ':GoInstallBinaries' }
call plug#end()

call plug#begin()
  Plug 'preservim/nerdtree'
call plug#end()
```
- Run install command on neovim:
```console
:PlugInstall
```
5. Run GoInstallBinaries
```console
:GoInstallBinaries
```

6. Install completion:
```console
:CocInstall coc-go
```

6. Create go file:
```console
nvim main.go
```

7. Init project:
```console
go mod init helloworld
```

8.  Create main file:
```console
nvim main.go
```

9. Add main.go content:
```go
package api

import "fmt"

func main() {
	fmt.Println("Enjoy!!!")
}
```
```
:GoRun
```

10. Enjoy
```console
Enjoy!!!
```

# Useful commands
> ctrl w w : switch between tree and file
> t: open in new tab (it works standing on the tree)
> :xa close all
> type m from nerdtree to see possible actions like create file
Extra: you can follow the [vim-go tutorial](https://github.com/fatih/vim-go/wiki/Tutorial)