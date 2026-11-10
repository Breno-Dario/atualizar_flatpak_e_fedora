<img align="left" width="100" height="100" hspace="15" alt="fedora" src="https://github.com/user-attachments/assets/88ec2f14-36a6-4b78-82a5-7d8030f522a7"/> 



# Script de atualização do Fedora e flathub
![Shell](https://img.shields.io/badge/Shell-✔️-red)
![License](https://img.shields.io/badge/License-MIT-lightgrey)
![Tests](https://img.shields.io/badge/Tests-✔️-green)
![void Linux](https://img.shields.io/badge/FEDORA-✔️-blue)


Este script em Bash automatiza tarefas comuns de manutenção no sistema utilizando de pacotes `dnf` e pacotes `flatpak` (usado no fedora)

## ⚙️ Funcionalidades 

O script executa as seguinte estapas:

1. **Atualiza a lista de repositórios**
2. **Atualiza todos os pacotes do sistema**
3. **Faz a reiniciação do sistema**
4. **Exibe mensagens de status para cada etapa**

## 💻 Descrições dos comandos

1. Primeiro você deve criar um arquivo `.sh` do script que possa roda no fedora
   Exemplo: 

```bash
   nano atualizar_flatpak_e_fedora
```

2. Segundo adicionar o `bin/bash` para que os comnados seja reconhecido pelo terminal

```bash
  #!/bin/bash
```
 
3. Terceiro adicionar `echo` = (tipo String) com descrição da ação que será efetuada

```bash
   echo "Atualizando repositório..."
```
4. Quarto adicionar comando do próprio fedora como atualizar

```bash
  sudo dnf update -y
```

5. Quinto criar uma condicional para perguntar se é necessário reiniciar o sistema

```bash
read -r -p "Deseja reinicar o notebook (y/n): " execucao

case $execucao in

	y | Y | yes | YES | Yes )
	echo "Reiniciando sistema..."
	systemctl reboot
	;;
	
	n | N | no | No | NO )
	echo "Reiniciamento cancelado..."
	exit 1
	;;

	*)
	echo "Entrada inválida. Por favor digite Y ou N para reiciniar ou não."
	exit 1
	;;
esac 
```

 ## Script completo: 
```bash
echo -e "\n==================================="
echo -e "\n  -- Atualizando Reposítorio --  \n"
echo -e "===================================\n"
sudo dnf update -y

echo -e "\n==================================="
echo -e  "\n    -- Aplicando atualização -- \n"
echo -e "===================================\n"
sudo dnf upgrade -y

echo -e "\n==================================="
echo -e "\n      -- Limpeza de cache --    \n"
echo -e "===================================\n"
sudo dnf clean all  

echo -e "\n==================================="
echo -e "\n      -- Atualização Flatpak --    \n"
echo -e "===================================\n"
sudo flatpak update -y

echo -e "\n=================================="
echo -e  "n  -- Reniciar notebook --  \n"
echo -e "===================================="

read -r -p "Deseja reinicar o notebook (y/n): " execucao

case $execucao in

	y | Y | yes | YES | Yes )
	echo "Reiniciando sistema..."
	systemctl reboot
	;;
	
	n | N | no | No | NO )
	echo "Reiniciamento cancelado..."
	exit 1
	;;

	*)
	echo "Entrada inválida. Por favor digite Y ou N para reiciniar ou não."
	exit 1
	;;
esac 

echo -e "\n == LIMPEZA E ATUALIZAÇÃO APLICADA COM SUCESSO =="
```
## 🛠️ Execução

Criando o script corretamente, você deve dar permisão de execução

```bash
chmod x+ atualizar_flatpak_e_fedora
```
Por fim pode executar o script dessa forma 
```bash
./atualizar_flatpak_e_fedora.sh
```
