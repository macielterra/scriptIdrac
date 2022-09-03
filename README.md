# scriptIdrac
Script para acessar IDrac6

Passos para criação do Script Idrac 6

1 - Instalar JRe 1.7.0.80
2 - Baixar arquivo .jnlp do Console Idrac(Launch).
3 - Abrir o .jnlp com editor de texto
4 - Localizar a linha no .jnlp onde informa para baixar os arquivos .jar do seu S.O.(Fazer o Download)
5 - Localizar a linha no .jnlp onde informa para baixar os arquivos .lib(.so) do seu S.O.(Fazer o Download)
6 - Após todos baixados e descompactados dentro do mesmo diretorio
7 - criar um shell com o seguinte conteúdo
#!/bin/bash

echo -n 'Host: '
read drachost

echo -n 'Username: '
read dracuser

echo -n 'Password: '
read -s dracpwd
echo

./jre/bin/java -cp avctKVM.jar -Djava.library.path=./lib com.avocent.idrac.kvm.Main ip=$drachost kmport=5900 vport=5900 user=$dracuser passwd=$dracpwd apcp=1 version=2 vmprivilege=true "helpurl=https://$drachost:443/help/contents.html"

8 - Salve com o nome start-virtual-console.sh
9 - Dê as permissões de execução ao sh
10 - Libere a porta 6000.
     iptables -I INPUT -p tcp --dport 6000 -j ACCEPT
     iptables -nL |grep 6000(Verifica se foi liberada)
11 - Export a variável display
     export DISPLAY=:0.0
12 - Acesse o arquivo de configuração do seu gerenciador de desktop.
     Ex: /etc/gdm3/custom.conf
         na seção"XDMCP"
           insira: "Enable=true"(Libera o protocolo de acesso via X11)
13 - Logado com seu usuário execute o comando 
     Xhost+ ou Xhost
14 - aplica o comando "su - user" para obter acesso a sessão remota.

Pronto, só executar o script criado. 
Obs: ao rodar o script ele solicita o HOST="IP" - USER="Login remoto" - PASSWD="Senha remota"
Exibirá o terminal do Idrac.
