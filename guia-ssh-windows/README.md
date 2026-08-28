# 🚀 **Tutorial para conectar seu GitHub ao Windows via SSH**
Se você usa Windows e quer mais praticidade — sem perder o controle e a segurança ao enviar seus códigos pro GitHub — e de quebra eliminar a necessidade de digitar senhas a cada ***push***: pensando no ***commit*** nosso de cada dia, *let's go*!

---
## 🛠️ Passo 0: **Baixando o Git Bash**
O Windows não vem com o terminal Bash por padrão. Então caso você não tenha esse terminal precisará baixar e instalar o **Git for Windows**- que já inclui o **Git Bash**.  *Siga meus bons* neste passo-a-passo bem basicão:
-1. Vamos ao site oficial do [Git for Windows](https://git-scm.com/download/win) e bora fazer o download do instalador.
-2. Execute o arquivo baixado e avance nas telas - *pode manter todas as opções padrão marcadas durante a instalação*.
-3. Finalizou?! Agora é só abrir o menu Iniciar do Windows, pesquisar por **Git Bash** e clicar para abrir o terminal.
---
*Que comecem os jogos!*
## **Assimilando o Conceito com Zero chances de Compilação** 😎
Vamos pensar  que o SSH é um **cadeado com duas chaves**:
1. **Chave Pública (`.pub`):** É o seu *cadeado*. Você pode entregar para o GitHub sem medo.
2. **Chave Privada:** É a sua *chave física*. Ela fica guardada de forma secreta no seu computador.
Quando você tenta enviar um código, o GitHub usa o seu "cadeado" (*chave pública*) e o seu computador usa a "chave privada" para abrir a conexão. Se baterem certinho, o acesso é liberado!
---
## 🛠️ **Agora é mão no teclado e terminal aberto: Passo a Passo Prático no Windows**
### 1. Gerando suas Chaves
No terminal **Git Bash**, digite o comando abaixo trocando pelo seu e-mail cadastrado no GitHub:
```bash
ssh-keygen -t ed25519 -C "seu-email@exemplo.com"
![Chave SSH 🤩](assets/ChaveSSH.documentacao.jpg)
💡 O terminal vai fazer algumas perguntas. Pode pressionar Enter em todas para aceitar as configurações padrão.
2. Copiando a chave pública gerada
Mostre o conteúdo da chave no terminal e copie o texto exibido:
Snippet de código

cat ~/.ssh/id_ed25519.pub
![cat da chave](assets/ChaveSSH.documentacao-2.jpg)
3. Ligando o "Agente de Segurança" (SSH Agent)
Para que o Windows gerencie suas chaves em segundo plano, execute:
Snippet de código

eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
	💡 Já tem uma chave criada? Se você já criou uma chave SSH neste computador anteriormente, não precisa rodar o comando de geração novamente. Basta ir direto para o Passo 4 e copiar sua chave existente!
4. Adicionando a chave no seu GitHub
Agora você vai acessar o seu GitHub através do navegador. Faça o seguinte:
1.Clique na sua foto de perfil (canto superior direito) > Settings.
2.No menu lateral esquerdo, clique em SSH and GPG keys.
3.Clique no botão verde New SSH key.
![Nova SSH](assets/ChaveSSH.documentacao-3.jpg)
4.Cole o conteúdo no campo Key e dê um título (ex: PC Pessoal).
![Colando SSH](assets/ChaveSSH.documentacao-4.jpg)
5.Clique em Add SSH key.
![SSH Salva](assets/ChaveSSH.documentacao-5.jpg)
5. Testar se a conexão SSH com o GitHub está funcionando
Snippet de código

ssh -T git@github.com
![Git teste](assets/ChaveSSH.documentacao-6.jpg
6. Finalmente conectando e clonando seu repositório diretamente do Terminal
Agora você pode clonar o repositório usando a URL em formato SSH
Snippet de código
![Git clone](assets/ChaveSSH.documentacao-8.jpg

git clone git@github.com:SEU-USUARIO/SEU-USUARIO.git
💡* Uma curiosidade sobre a porta 22 usada para trafegar as informações no formato SSH Essa porta é o canal padrão de rede reservado mundialmente para o protocolo SSH (Secure Shell). Pense na porta como um "crachá de acesso" ou uma tomada específica no servidor destinada apenas a conexões criptografadas de terminal/administração.Os dados do seu código e commits trafegam 100% criptografados pela rede. Mesmo que alguém intercepte os pacotes no meio do caminho, não conseguirá ler o conteúdo. Sem a chave privada correspondente instalada na sua máquina, ninguém consegue se passar por você ou enviar código para seus repositórios. Uma vez configurada a chave SSH no seu computador e na sua conta do servidor, você não precisa digitar login ou senha a cada git push ou git pull.*
🚨 ##Troubleshooting: Resolvendo Erros Comuns Mesmo seguindo o passo a passo, alguns erros comuns podem acontecer no Windows:
❌### Erro: fatal: protocol 'git@github.com:https' is not supported O que significa: Esse erro acontece quando o Git tenta interpretar a URL fornecida e encontra uma mistura de dois protocolos diferentes (SSH e HTTPS) no mesmo endereço. Apenas apague o início (https) do seu endereço ao clonar.
![Git clone Error](assets/ChaveSSH.documentacao-7.jpg
❌### Erro: Could not open a connection to your authentication agent O que significa: O serviço que guarda as chaves no Windows não iniciou. Como resolver: Lembre-se de rodar eval "$(ssh-agent -s)" antes de adicionar a chave.
✅ Testando se Deu Certo Para testar a conexão final, digite no Git Bash:
Snippet de código

ssh -T git@github.com
![Success Full](assets/ChaveSSH.documentacao-9.jpg)
Sucesso: Se aparecer a mensagem Hi [Seu-Usuario]! You've successfully authenticated..., parabéns! Seu ambiente está configurado e seguro. 🎉

