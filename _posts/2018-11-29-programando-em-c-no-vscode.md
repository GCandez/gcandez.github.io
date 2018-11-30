---
layout: post
title:  "Programando em C no Visual Studio Code"
date:   2018-11-29 23:11:25 -0200
categories: programacao c
---
# Instalando um compilador #
Existem diversos compiladores disponíveis: **gcc**, **clang**, **msvc**. Utilizaremos neste tutorial o **gcc**, mais especificamente o **mingw-w64**, que é uma versão para o Windows que oferece versões em 32 e 64 bits.

Usuaremos a distribuição do **mingw-w64** presente no **MSYS2**

## MSYS2 ##

O **MSYS 2** é uma distribuição de ferramentas e plataforma de compilação para o Windows.

### Passo 1: Instalando o MSYS 2 ###

O **MSYS2** conta com um simples instalador que pode ser encontrado no [site oficial](http://www.msys2.org/).

![Site do MSYS2](/assets/msys2_website.png)

Caso seu sistema seja 32 bits, baixe o arquivo `msys2-i686`, ou `msys2-x86_64`.

1. [Baixe o instalador](http://www.msys2.org/)
    * Para sistemas **32bits**: `msys2-i686`
    * Para sistemas **64bits**: `msys2-x86_64`
2. Execute o instalador
3. Clique em **Next**
    
    ![](/assets/msys2_install_1.png)
4. Selecione o local onde serão instalados os arquivos. Nesse exemplo usaremos o padrão que é `C:\msys64` (para a versão 32 bits o padrão é `C:\msys32`), porém você pode escolher outro local

    ![](/assets/msys2_install_2.PNG)
5. Após terminar a instalação, clique em **Finish**

    ![](/assets/msys2_install_3.PNG)

Foram adicionados ao **Menu Inicial** 3 novos atalhos:

* **MSYS2 MinGW 64-bit**: Abre um terminal cujo ambiente é o **MinGW 64**
* **MSYS2 MinGW 32-bit**: Abre um terminal cujo ambiente é o **MiNGW 32**
* **MSYS2 MSYS**: Abre um terminal cujo ambiente é o **MSYS**

Para instalar atualizações e novos pacotes, utilize apenas o `MSYS2 MSYS`. Os outros dois terminais dão acesso as ferramentas/executáveis do MinGW.

### Passo 2: Atualizando o MSYS 2 ###

Antes de adicionarmos o **gcc**, precisamos atualizar nosssa instalação do **MSYS2**. O processo de atualização é extremamente simples.

1. Abra o terminal `MSYS`

    ![](/assets/msys2_update_1.png)
2. Digite `pacman -Syuu` e responda `Y` quando perguntado se deseja prosseguir com a instalação.

    ![](/assets/msys2_update_2.png)

    ![](/assets/msys2_update_3.png)

3. Reinicie o terminal e execute novamente o comando do passo anterior. Repita esse passo (reiniciando o terminal cada vez) até que tudo tenha sido atualizado.
    
    ![](/assets/msys2_update_4.png)


### Passo 3: Instalando o GCC ###

1. Abra o termina `MSYS2 MSYS`
2. Execute o comando:
    * Para 32 bits: `pacboy sync mingw-w64-i686-gcc`
    * Para 64 bits: `pacboy sync mingw-w64-x86_64-gcc`

    ![](/assets/msys2_gcc_1.png)
3. Instale também o **gdb**, que é utilizado para debugar:
    * Para 32 bits: `pacboy sync mingw-w64-i686-gdb`
    * Para 64 bits: `pacboy sync mingw-w64-x86_64-gdb`

    ![](/assets/msys2_gcc_2.png)
4. Verifique se o *gcc* e *gdb* foram instalador com sucesso. Para isso abra o terminal `MSYS2 MinGW` (32 ou 64 bits, abra o referente à do gcc que você instalou).
    * Verifique o *gcc*: `gcc --version`
    * Verifque o *gdb*: `gdb --version`

    ![](/assets/msys2_gcc_3.png)

Por útlimo, iremos adicionar o diretório contendo os executáveis do **gcc** e do **gdb** na variável `PATH` do sistema. Isso permite que você execute o comando **gcc** ou **gdb** no terminal do windows, em qualquer diretório.

1. Vá nas propriedades de `Meu Computador`, clique em `Configurações avançadas do sitema`, vá na aba `Avançado` e clique em `Variáveis de Ambinete`

    ![](/assets/path_1.png)
2. Na lista que apareceu, selecione a variável `Path` clique em `Editar`

    ![](/assets/path_2.png)

3. Clique em `Novo` e adicione:
    * Caso tenha instalado o **GCC 32bits**: `C:\msys64\mingw32\bin`
    * Caso tenha instalado o **GCC 64bits**: `C:\msys64\mingw64\bin`
    * Caso não tenha instalado o **MSYS2** no diretório padrão não tem problema! Por exemplo, caso tenha instalado em `D:\msys`, o caminho para o **GCC 32bits** seria `D:\msys\mingw32\bin` e para o **GCC 64bits** seria `D:\msys\mingw64\bin`

    ![](/assets/path_3.png)
4. Feche as janelas clicando em `OK`.
5. Abra um novo terminal do windows (<kbd>Windows</kbd>+<kbd>R</kbd> e digite `cmd`)
6. Verifique se consegue executar os comandos `gcc --version` e `gdb --version`.
    
    ![](/assets/path_4.png)
    * Caso não consiga executar os comandos, reinicie seu computador.
    * Se mesmo após reiniciar não consegue executar os comandos, certifique-se que adicionou os caminhos corretos no passo **3**

Agora você tem um compilador instalado e disponível para ser utilizado!

# Instalando e configurando o Visual Studio Code #

## Passo 1: Instalando o Visual Studio Code ##
O Visual Studio Code (VS Code) é um excelente editor de código que possuí diversas extensões para linguagens como **PHP**, **C**, **Java**, **C#** e muitas outras.

Para instalar o VS Code, baixe o instalador no [site oficial](https://code.visualstudio.com/).

![Site oficial do VS Code](/assets/vscode_website.png)

## Passo 2: Instalando a extensão C\C++ ##
Após instalar o VS Code, clique no botão de extensões e adicione a extensão `C\C++`

![](/assets/cpp_extension.jpg)

Reinicie o VS Code.

## Passo 3: Programando em C ##
Faremos um simples *Olá Mundo*.
Primeiro, recomendo que crie uma pasta para cada projeto. Você pode clicar com o botão direito em qualquer pasta para abri-la no VS Code.

Primeiro precisamos configurar a extensão `C\C++` para o nosso projeto.

1. Aperte <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd>, digite `cpp` e selecione a opção `C/Cpp: Edit Configurations...`
2. Um arquivo chamado `c_cpp_properties.json` irá abrir, copie o conteúdo abaixo e cole no seu arquivo
* Substitua o caminho em `compilerPath` para o caminho do executavel gcc. Caso tenha instalado o gcc 64 bits, com o MSYS2 64bits instalado no diretório padrão, esse caminho será `C:\msys64\mingw64\bin\gcc.exe`. Note que é preciso substituir a barra invertida `\` por duas `\\`.
{% highlight json %}
{
    "configurations": [
        {
            "name": "MinGW",
            "intelliSenseMode": "gcc-x64",
            "compilerPath": "C:\\msys64\\mingw64\\bin\\gcc.exe",
            "includePath": [
                "${workspaceFolder}"
            ],
            "defines": [],
            "cStandard": "c11"
        }
    ],
    "version": 4
}
{% endhighlight %}

Agora com a extensão configurada, crie um arquivo com extensão `.c`, e nele escreveremos nosso código.

![](/assets/vscode_1.png)

Agora, precisaremos configurar uma tarefa (task) para compilar nosso código.

1. Aperte <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd>, digite `task` e selecione a opção `Task: Configure Default Build Task`
2. Selecione a opção `Create tasks.json...` e em seguida `Others`
3. Será aberto um arquivo `tasks.json`, copie o conteúdo abaixo e cole em seu arquivo.
{% highlight json %}
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "Compilar",
            "type": "shell",
            "command": "gcc.exe teste.c",

            "group": {
                "kind": "build",
                "isDefault": true
            },
            "problemMatcher": "$gcc"
        }
    ]
}
{% endhighlight %}

Para testar sua tarefa de compilação, aperte <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>P</kbd>, digite `build` e selecione a opção `Tasks: Run Build Task`, ou então aperte <kbd>Ctrl</kbd>+<kbd>Shift</kbd>+<kbd>B</kbd>

Verifique se foi gerador um arquivo `a.exe` na mesma pasta que seu arquivo `.c`, execute-o e verifique se seu código funciona.

O próximo passo é configurar o debug.

1. Aperte <kbd>F5</kbd> e selecione a opção `C++ (GDB\LLDB)`
2. Será aberto um arquivo `launch.json`, copie o conteúdo abaixo para seu arquivo:
{% highlight json %}
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "(gdb) Launch",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/a.exe",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": true,
            "MIMode": "gdb",
            "miDebuggerPath": "gdb.exe",
            "setupCommands": [
                {
                    "description": "Enable pretty-printing for gdb",
                    "text": "-enable-pretty-printing",
                    "ignoreFailures": true
                }
            ]
        }
    ]
}
{% endhighlight %}

Agora, ao apertar <kbd>F5</kbd> o VS Code iniciará uma sessão de debug do seu programa.