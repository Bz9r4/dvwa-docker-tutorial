🇧🇷 Leia em [Português](README.md) | 🇺🇸 Read in [English](README_EN.md)

# Como Instalar DVWA usando Docker no Ubuntu

## Requisitos
- Um sistema operacional baseado em Linux (Ubuntu recomendado)
- Conexão com a internet

## Passo 1: Atualizar o Sistema
Antes de instalar qualquer coisa, é uma boa prática atualizar o sistema:
```bash
sudo apt update && sudo apt upgrade -y
```

## Passo 2: Instalar Dependências
Instale os certificados necessários para baixar e instalar o Docker corretamente:
```bash
sudo apt-get install ca-certificates curl
```

## Passo 3: Adicionar a Chave GPG do Docker
Crie o diretório necessário e baixe a chave GPG do Docker:
```bash
sudo install -m 0755 -d /etc/apt/keyrings
```
```bash
sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg -o /etc/apt/keyrings/docker.asc
```
```bash
sudo chmod a+r /etc/apt/keyrings/docker.asc
```

## Passo 4: Adicionar o Repositório do Docker
Adicione o repositório oficial do Docker à lista de fontes do sistema:
```bash
echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.asc] https://download.docker.com/linux/ubuntu \
  $(. /etc/os-release && echo "$VERSION_CODENAME") stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
```

## Passo 5: Instalar o Docker
Agora instale o Docker e seus componentes:
```bash
sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
```
Durante a instalação, pressione `Y` para confirmar o download dos pacotes necessários.

## Passo 6: Testar a Instalação do Docker
Para garantir que o Docker foi instalado corretamente, execute:
```bash
sudo docker run hello-world
```
Se tudo estiver correto, você verá uma mensagem indicando que o Docker está funcionando.

## Passo 8: Iniciar e Habilitar o Docker
Ative o serviço do Docker para iniciar automaticamente com o sistema:
```bash
sudo systemctl start docker
```
```bash
sudo systemctl enable docker
```

## Passo 8: Permitir Uso do Docker sem `sudo`
Adicione seu usuário ao grupo `docker` para evitar a necessidade de usar `sudo` sempre:
```bash
sudo usermod -aG docker $USER
```
Reinicie a sessão para que as permissões sejam aplicadas corretamente.

## Passo 9: Baixar e Rodar o DVWA
Agora que o Docker está configurado, podemos baixar a imagem do DVWA:
```bash
docker pull vulnerables/web-dvwa
```
Execute o contêiner do DVWA na porta 80:
```bash
docker run -d -p 80:80 vulnerables/web-dvwa
```
## passo 10: Execute docker ps para ver se o container está rodando corretamente
```bash
docker ps
```

## Passo 11: Acessar o DVWA

1. No seu navegador, acesse `http://SEU_IPV4`.
2. Na tela de login, apenas clique em **Login** sem preencher os campos.
3. Na tela de configuração, role até o final e clique em **Create/Reset Database**.
     Esse botão é responsável por:
   
          - Criar a estrutura inicial do banco de dados do DVWA.
          - Criar as tabelas necessárias para armazenar usuários, configurações e logs dos testes de vulnerabilidade.
          - Garantir que o ambiente está pronto para uso, eliminando quaisquer inconsistências ou dados antigos.
4. A tela de login aparecerá novamente. Use as credenciais:
   - **Username:** `admin`
   - **Password:** `password`

Agora, o DVWA está pronto para ser usado! 🎉

---
Esse guia deve ajudá-lo a configurar rapidamente um ambiente seguro para testes de segurança no Ubuntu.

