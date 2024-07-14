# Virtualização de máquina para um ambiente virtual

---

- [x] - Sobre a documentação:

Documentação para virtualizar com o WSL 2 o Linux no Windows. Essa é uma virtualização que fica mais leve, principalmente para máquinas que tem um valor igual ou menor de 8GB de RAM e não tem uma performance tão boa com máquinas virtuais, como um Hyper-V do próprio Windows ou uma VirtualBox da Oracle. 

Também iremos instalar o Python juntamente deste tutorial, pois pode ser também do nosso interesse.

Notar que você deve estar executando o Windows 10 versão 2004 e superior (Build 19041 e superior) ou o Windows 11.

### Nota: Este tutorial também pode ser executado utilizando uma máquina virtual como o Hyper-V ou VirtualBox, pois, os comandos são muito semelhantes.

---

## Pré Requisitos para utilização da WLS 2:

* Você deve estar executando o Windows 10 versão 2004 e superior (Build 19041 e superior) ou o Windows 11.

* Para verificar a versão e o número de build do seu Windows, selecione a tecla do logotipo do Windows + R, digite winver e selecione OK. Você pode atualizar para a versão mais recente do Windows no menu Configurações ou usando o Assistente do Windows Update.

* Se você estiver executando um build mais antigo ou simplesmente prefere não usar o comando para instalar e quer instruções passo a passo, confira Etapas de instalação manual do WSL para versões mais antigas, que estão nessa documentação.

--- 

## Inicio do bloco para virtualização do Linux no Windows com WSL (Subsistema do Windows para Linux).

Iremos utilizar uma virtualização no Windows chamada WSL 2, que não possuí todas distribuições do Linux como um Hyper-V ou uma máquina virtual convencional, porém, irá atender este projeto.

1º - Instalação da WSL 2 para virtualização do Linux no Windows, da maneira mais prática e simplista para caso você esteja com a versão mais recente do build do Windows. Caso tenha essa última versão, é só executar o comando abaixo e que executa as seguintes opções:
  - Habilita os componentes opcionais WSL e Plataforma de Máquina Virtual.
  - Baixa e instala o kernel do Linux mais recente.
  - Define WSL 2 como o padrão.
  - Baixa e instala a distribuição Ubuntu Linux aplicativo (a reinicialização pode ser necessária).
  ```powershell
  wsl --install
  ```
  
  Documentação de referência: https://docs.microsoft.com/pt-br/windows/wsl/install
  
  ---
  
  2º - Instalação da WSL 2 para virtualização do Linux no Windows caso você esteja com um build mais antigo do Windows, ou seja, não esteja com o build atual.
  
   - Etapa 1 – Habilitar o Subsistema do Windows para Linux:
   
     - Antes de instalar qualquer distribuição do Linux no Windows, você precisará primeiro habilitar o recurso opcional "Subsistema do Windows para Linux".

     - Abra o PowerShell como administrador e execute:
     
     ```powershell
     dism.exe /online /enable-feature /featurename:Microsoft-Windows-Subsystem-Linux /all /norestart
     ```
     
   - Agora, é recomendável passar para a etapa 2, de atualização para o WSL 2. Mas, se você desejar instalar apenas o WSL 1, será possível reiniciar o computador e passar para a Etapa 6 – Instalar a distribuição do Linux de sua escolha. Para atualizar para o WSL 2, aguarde o seu computador ser reiniciado e passe para a próxima etapa.
  
  ---
  
  - Etapa 2 – Verificar os requisitos para executar o WSL 2:
  
  - Para atualizar para o WSL 2, você precisa estar executando o Windows 10.

    - Para sistemas x64: Versão 1903 ou superiores, com o Build 18362 ou superiores.
    
    - Para sistemas ARM64: Versão 2004 ou superiores, com o Build 19041 ou superiores.
    
    - Os builds inferiores a 18362 não dão suporte a WSL 2. Use o Assistente do Windows Update para atualizar a sua versão do Windows.
    
    - Para verificar a sua versão e o número de build, selecione a tecla do logotipo do Windows + R, digite winver e selecione OK. Atualize para a versão mais recente do Windows no menu Configurações.
    
    ---
    
   - Etapa 3 – Habilitar o recurso de Máquina Virtual
    
     - Antes de instalar o WSL 2, você precisa habilitar o recurso opcional Plataforma de Máquina Virtual. Seu computador exigirá funcionalidades de virtualização para usar esse recurso.

     - Abra o PowerShell como administrador e execute:
     
     ```powershell
     dism.exe /online /enable-feature /featurename:VirtualMachinePlatform /all /norestart
     ```
     
   ## Reinicie o computador para concluir a instalação do WSL e a atualização para o WSL 2.     
---
     
   - Etapa 4 – Baixar o pacote de atualização do kernel do Linux
   
   1. Baixar o pacote mais recente:
   
   - Pacote de atualização do kernel do Linux do WSL2 para computadores x64 - Baixe no site da documentação oficial -> https://docs.microsoft.com/pt-br/windows/wsl/install-manual
   
   2. Execute o pacote de atualização baixado na etapa anterior. (Clique duas vezes para executar. Você receberá uma solicitação para fornecer permissões elevadas; selecione 'sim' para aprovar essa instalação).
   
   - Depois que a instalação for concluída, vá para a próxima etapa: configurar o WSL 2 como a sua versão padrão ao instalar novas distribuições do Linux (ignore essa etapa se você quiser que as novas instalações do Linux sejam definidas como WSL 1).
   
   ---
   
   - Etapa 5 – Definir o WSL 2 como a sua versão padrão:
   
     - Abra o PowerShell e execute este comando para definir o WSL 2 como a versão padrão ao instalar uma nova distribuição do Linux:
     ```powershell
     wsl --set-default-version 2
     ```  
   ---
   
   - Etapa 6 – Instalar a distribuição do Linux de sua escolha:
   
   1. Abra a Microsoft Store e escolha sua distribuição do Linux favorita. Neste caso estamos utilizando a Ubuntu para o projeto, mas fique á vontade para escolher.
   
   2. Na página da distribuição, selecione "Obter".
   
   - Na primeira vez que você iniciar uma distribuição do Linux recém-instalada, uma janela de console será aberta e será solicitado que você aguarde um ou dois minutos para que os arquivos sejam descompactados e armazenados em seu PC. Todas as futuras inicializações deverão levar menos de um segundo.

   - Em seguida, você precisará criar uma conta de usuário e uma senha para sua nova distribuição do Linux.
   
   ![image](https://user-images.githubusercontent.com/57469401/135000594-26d754ea-a2d4-4451-8b77-ee0da3326204.png)
 
  3. Abra a Microsoft Store e procure por "Windows Terminal", clique em "Obter" e "Instalar". Com esse terminal é possível rodar a distribuição que foi feita o download no item (1) anterior e é um terminal mais prático e acessível para quem está começando.
  
   - Instalação finalizada e distribuição Linux totalmente integrada ao sistema operacional Windows.

   - Nota: Se você quiser desinstalar a WSL 2 e a distribuição do Ubuntu, é só desinstalar como um programa convencional do Windows no Painel de Controle.

Documentação de referência: https://docs.microsoft.com/pt-br/windows/wsl/install-manual

## Fim do bloco para virtualização do Linux no Windows com WSL (Subsistema do Windows para Linux).

---

## Inicio do bloco para configurações no ambiente Linux.

1º - Abra o Windows Terminal como administrador.

---

2º - Deixe uma guia aberta com o PowerShell e uma com Ubuntu ou a distribuição que foi feita a instalação de sua escolha.

---

3º - Com os terminais abertos no modo administrador, iremos conectar o usuário (root) no terminal do Linux, pois, realizando testes com o usuário convencional na minha máquina, notei que pacotes de instalação estavam falhando e impedindo o funcionamento do Apache Airflow, logo, ao tentar com o usuário (root) funcionou perfeitamento. Passos abaixo para acessar o usuário (root) pela primeira vez.

  - No terminal digite o comando abaixo:
```linux
sudo passwd root # Primeiramente é necessário alterar a senha para uma de sua preferência.
```

  - Após alterar a senha utilize o comando abaixo para entrar no usuário (root). É um comando bem simples mesmo para acessar:
```linux
su # Após alterar a senha, utilize este comando para acessar o usuário root.
```

  - Para sair do usuário (root) e voltar ao usuário convencional digite o comando abaixo:
```linux
exit
ou
CTRL+D
```

## Nota: Todo o processo á partir de agora será relizado com o usuário (root) visando garantir o sucesso da instalação. Permaneça com o usuário (root).
---

4º - Configurando e ajustando os parâmetos conexão com a internet. Pontos importantes abaixo:

   - Máquinas que possuem VPN, como por exemplo uma Cisco, é possível que a internet não funcione de primeira, porém, por exemplo, na minha máquina, após utilização frequente do WSL, passou a funcionar, mas de primeira não foi assim.
   
   - Caso o item abaixo (I) ocorra com sucesso, não será necessário a execução do item (II). 

   - Caso o item abaixo (I) não ocorra com sucesso por conta da VPN, será necessário a execução do item (II), que fará uma configuração.

   - Faça o item abaixo (I) tanto com a VPN ligada, quanto com a VPN desligada, pois, em alguns casos a conexão com a internet só funciona com um desses tipos (VPN ligada ou desligada).

I. Realizar um teste de conexão com o comando abaixo no terminal do Linux. Caso o comando seja executado com sucesso e com retorno de rede, não será necessário executar o passo II.
```linux
ping google.com
```

II. Abra o PowerShell e execute os comandos abaixo.
```powershell
Get-NetIPInterface -InterfaceAlias "vEthernet (WSL)" | Set-NetIPInterface -InterfaceMetric 1  #Esta linha seta a interface do WSL como uma das principais.
Get-NetAdapter | Where-Object {$_.InterfaceDescription -Match "Cisco AnyConnect"} | Set-NetIPInterface -InterfaceMetric 6000  #Esta linha diminui a prioridade da rede VPN, para ficar menor do que a rede virtual WSL.
```
Após executar esses dois comandos no PowerShell, abra o temrinal do Linux e realize um teste de conexão com os comandos abaixo. Notar que não é obrigatório testar a linha com (ping minha.intranet), pois, como iremos utilizar o Apache Airflow local, não seria necessário conexão com essa rede, porém, se você possuir VPN e quiser testar fique á vontade, porém, o que realmente importa é que linha (ping google.com) funcione com retorno de rede.
```linux
ping google.com
ping minha.intranet #Nesta linha em vez de executar uma url como o google, teste uma url que só funciona conectado a VPN.
```

Caso os comandos e os testes sejam executados com sucesso, agora estamos com acesso a rede e podemos seguir para os próximos passos.

---

5º - Abra o terminal Linux e digite o comando abaixo para atualizar e realizar um upgrade se necessário no ambiente virtualizado do Linux.
```linux
sudo apt update && sudo apt upgrade
```
Notar que também podemos executar os comandos separadamente conforme abaixo:
```linux
sudo apt-get update
sudo apt-get upgrade
```
---

6º - Instalação do pip para o Python, que por padrão não vem instalado no Linux. Execute o comando abaixo no terminal do Linux. Notar que estamos diretamente indicando o Python na linha da versão 3, pois, por indicação é bom manter e utilizar a linha da versão 3, pois, por exemplo, nas máquinas virtuais da AWS, o padrão é o Python na linha das versões 3.
```linux
sudo apt-get install python3-pip
```
---

7º - Execute o comando abaixo no terminal do Linux para verificar se a instalação do pip foi concluída com sucesso, onde está instalado e para qual versão do Python. Notar que o (V) do comando é maiúsculo.
```linux
pip -V
```
---

8º - Instalação da virtualenv para construir o ambiente virtual do Python e mais duas extensões para garantir o funcionamento das bibliotecas. Execute o comando abaixo no terminal do Linux.
```linux
sudo pip3 install virtualenv
sudo apt-get install python3-dev
pip3 install wheel
```

9º - Criação de um repositório (pasta) em algum local de sua preferência, mas neste caso iremos criar na área de trabalho para melhorar a didática. Podemos criar manualmente e diretamente na área de trabalho, ou pelo terminal do Linux. Neste caso iremos criar pelo terminal. Execute os comandos pelo terminal do Linux.
```linux
cd Desktop
mkdir Projeto
cd Projeto
mkdir Pipeline
cd Pipeline
```

Pronto, agora temos os repositórios criados.

---

10º - Criação da virtualenv no repositório (Pipeline), que foi criado no passo anterior. O nome do repositório, neste caso, será (venv). Execute o comando abaixo no terminal do Linux.
```linux
sudo virtualenv venv
ou
python3 -m virtualenv venv
```
---

11º - Verificar se temos o repositório (venv) no repositório que destinamos a criação. Este comando verifica os repositórios abaixo do atual. Execute o comando abaixo no terminal do Linux.
```linux
ls
```
---

12º - Ativação da virtualenv para utilização. Notar que após executar o comando, aparecerá em parenteses (venv) ou o nome do repositório na linha de comando principal, querendo dizer que qualquer comando python executado a partir de agora irá rodar na virtual env. Execute o comando abaixo no terminal do Linux.
```linux
source venv/bin/activate
```

Ficará algo parecido com isso caso ocorra corretamente a ativação da virtualenv: 
```
(venv) usuario@local:/mnt/c/Users/zézinho/Desktop/Projeto/Pipeline$
```

Para desativar uma virtualenv, certifique-se que elá está ativada na linha de comando e execute o comando abaixo no terminal do Linux.
```linux
deactivate
```

Para exluir a virtualenv (tem que ser depois da desativação), você não pode estar no repositório da virtualenv, neste caso o (env), logo, é necessário voltar um repositório. Iremos considerar os repositórios criados para didática. Execute o comando abaixo no terminal do Linux.
```linux
cd ..
rm -r env
```

Para criar e ativar a virtualenv, execute novamente os passos de criação e ativação.

Nota: Recrie e ative a virtualenv, pois iremos utilizá-la. Lembre-se de manter o caminho de repositório que neste caso seria algo parecido com isso: 
```
(venv) usuario@local:/mnt/c/Users/zézinho/Desktop/Projeto/Pipeline$
```

---

Pronto, agora temos uma máquina virtualizada e com o Python instalado para utilização !

---

[Acesse meu GitHub :cat:](https://github.com/Phelipe-Sempreboni)

[Acesse meu LinkedIn :computer:](https://www.linkedin.com/in/luiz-phelipe-utiama-sempreboni-319902169/)

---

_Espero ajudar_ :smiley:
